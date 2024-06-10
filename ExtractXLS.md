# Extract XLS

### Description

This function is used to extract content from Excel files.

### Library requirements

* sanic
* logging
* asyncio
* io
* aiohttp
* base64
* random
* inspect
* openpyxl
* os
* math

You can install all requirements by running:

```agsl
pip3 install -r requirements.txt
```

or

```agsl
pip install -r requirements.txt
```

And now you can launch the app locally:

```agsl
python3 app.py
```

or

```agsl
python app.py
```

### Endpoint

/extract-excel

#### port: 8011

#### Headers

"Content-Type": "multipart/form-data"

#### Error Code

500 : Error in form data
415 : Format not allowed or unsupported

#### Input

Key: file  
Value: a XLS or XLSX or XLSM file

#### Output

JSON with the file name and a string list of content recognition

```json

{
    "file_name": "[Associations et Entreprises] Attestation de santé financière.xlsx",
    "result_extract_excel": [
        "La présente déclaration sur la santé financière certifie que la structure représentée par le signataire légal ou dûment habilité n'est pas une entreprise en difficulté au sens de la réglementation communautaire.\n\nSelon les informations fournies, la structure :\n\n- n'est pas une entreprise en difficulté au sens de la réglementation communautaire.\n\nOu, si la structure est une entreprise en difficulté :\n\n- est devenue une entreprise en difficulté au sens de la réglementation communautaire entre le 01/01/2020 et le 30/06/2021.\n- est devenue une entreprise en difficulté au sens de la réglementation communautaire après le 30/06/2021.\n\nSi la structure est une micro ou petite entreprise, elle :\n\n- est devenue en difficulté avant le 31/12/2021 et ne fait pas l'objet d'une procédure collective d'insolvabilité en vertu du droit national (sauvegarde, redressement ou liquidation judiciaires) ET n'a pas bénéficié d'une aide au sauvetage ou d'une aide à la restructuration.\n\nLa déclaration a été faite à [Lieu] le [Date].",
        "The image shows the official logo of the Republic of France, which consists of the French national flag (blue, white, and red vertical stripes) and the text \"REPUBLIQUE FRANCAISE\" (French Republic) below it. The text also includes the French national motto \"Liberté, Égalité, Fraternité\" (Liberty, Equality, Fraternity). 1. The image shows the official logo of the Republic of France.\n2. The logo consists of the French national flag, which has three vertical stripes in the colors blue, white, and red.\n3. The text \"REPUBLIQUE FRANCAISE\" (French Republic) is displayed below the flag.\n4. The French national motto \"Liberté, Égalité, Fraternité\" (Liberty, Equality, Fraternity) is also included in the logo. Extracting the knowledge from this image was relatively straightforward, as the logo clearly displays the key elements of the French national identity, including the flag, the country name, and the national motto. The information contained in the image is direct and easily identifiable, making the knowledge extraction task simple and straightforward."
    ]
}
```

![alt text](<Graph/ExtractXLS_graph.png>)

#### extract_excel

La fonction "extract_excel" prend en entrée le fichier Excel et retourne le résultat de l'extraction. 

On va tout d'abord ouvrir le fichier grâce à la librairie _openpyxl_ puis pour toute les feuilles du classeur, si la feuille n'est pas vide (vérifié grâce à la fonction "is_sheet_empty"), on va convertir les éléments de la feuille en CSV grâce à la fonction "sheet_to_csv_string". Ensuite, on va nettoyer la feuille en supprimant les lignes vide qui se trouve au début grâce à la fonction "delete_void_line_in_front_of_sheet" puis en supprimant toutes les colonnes vides grâce à la fonction "delete_all_blank_columns". On va ensuite calculer le nombre de token grâce à la fonction "count_tokens" de la classe **"Token Calculator"** pour les comparer au nombre de token max prédéfini. Si le nombre de token de la feuille est inférieur au nombre de token max, le CSV est envoyé à la fonction "generate_message_content" (sans ancien message) afin de générer la structure attendu par l'application **"CSV Interpreter"** qui s'occupe de générer une explication détaillé de la feuille. Si le nombre max de token est dépassé, la feuille est envoyé à la fonction "extract_long_sheet_page".

S'il y a des images dans le fichier, elles sont envoyé à l'application **"OCR Figure"**.

Si le type du resultat est une liste (résultat de la fonction "extract_long_sheet_page") alors, il est directement ajouté à la liste du résultat final. Sinon, on va utiliser la fonction "find_value_in dict" afin de récuperer le résultat de CSV Interpreter et de OCR Figure, qui vont se retrouver dans un dictionnaire s'il n'y a pas eu de découpage du fichier. 

#### extract_long_sheet_page

La fonction "extract_long_sheet_page" prend entrée une feuille du fichier CSV ainsi que son index et retourne le résultat dans une liste et l'index. 

On va tout d'abord séparer la feuille en fonction des lignes complètement vide grâce à la fonction "split_with_empty_line". Ensuite, le CSV séparé sera envoyé à la fonction "split_everything_with_max_token" pour séprarer la feuille en fonction du nombre maximum de token prédéfini. 

Pour chaque élément dans la liste de la feuille séparé, la fonction "generate_message_content" sera appliquer mais cette fois avec l'ancien message afin de garder le contexte du fichier et ne pas perdre le sens. 

Le résultat ainsi que l'index de la page seront envoyé à l'application **"CSV Interpreter"**. Le résultat est ensuite envoyé à la fonction "find_value_in_dict" puis retourner sous forme de liste avec l'index de la page. 

#### split_everything_with_max_token

La fonction "split_everything_with_max_token" prend entrée la liste avec les éléments de la feuille excel spliter en fonction des lignes vide ainsi que le nombre maximum de token. Elle retourne une liste avec les éléments spliter en fonction du nombre pas de token. 

On va tout d'abord calculer le nombre de token pour chaque élément de la liste. Si un élément est supérieur au max de token, il est renvoyé en mode récursif à la fonction "split_everything_with_max_token" avec en entrée l'élément spliter en fonction des sauts de ligne car le type de l'entrée est une liste. 

Ensuite, si le nombre de token de l'élément est respecté, il est ajouté à la liste du résultat.

#### generate_message_content

La fonction "generate_message_content" prend en entrée le contenue CSV ainsi que le messages précedent. Elle retourne le message précedent + le nouveau message. 

Cette fonction sert à structurer le message qui sera envoyé à l'application **"CSV Interpreter"** ainsi qu'à garder le contexte de la feuille. Le message précedent ainsi que le nouveau message seront envoyé à **"CSV Interpreter"** afin que Claude 3 puisse avoir le contexte (header, légende...) et expliquer au mieux les éléments. 

