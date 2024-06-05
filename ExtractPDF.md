# Extract PDF

### Description

This application allows us to extract content from PDF files.

### Library requirements

* pdfplumber
* asyncio
* aiohttp
* sanic
* logging
* os
* json
* inspect
* random

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
/extract-pdf

#### port: 8008

#### Headers :
"Content-Type": "multipart/form-data"

#### Input:
Key: file  
Value: a PDF file

#### Output :
a string list of content recognition

```
[
    "PAS D'ACCÈS À LA MESSAGERIE \nG3\nMÉTADONNÉES\nMESSAGERIE G3 ; APPLICATION WEB ; BOITE MAIL ; MOT DE PASSE\nDESCRIPTION\nLe restaurant nous contacte car il n’arrive plus à accéder à sa messagerie \nG3.",
    "SOMMAIRE\n1. Pas d’accès à la messagerie G3...................................................... .1\n1.1 Type d’incident.......................................................................... .1\n1.2 Réinitialisation des identifiants de connexion...................................1",
    "1. PAS D’ACCÈS À LA MESSAGERIE G3\n1.1 Type d’incident\nN°\nEtapes\n1\nLe restaurant arrive-il a accéder à la page de connexion sur la messagerie G3 ?\nOUI => Passer à la prochaine étape.\nNON => Suivre la procédure « Pas d'accès aux applications web sur le pc sir ».\n1.2 Réinitialisation des identifiants de connexion\n1\nRécupérer l’identifiant que le restaurant utilise pour s’y connecter.\n2\nEscalader le ticket dans le groupe « FR-REST-IN-INTERWAY » avec le proformat Messagerie G3 disponible sur l’outil Pronuaire du \nTSE."
]
```

### Controller

![alt text](<Graph/ExtractPDF_graph.png>)

Le fichier est envoyé à la classe **" Controller "** pour être analysé par la classe **" CheckType "** afin de
déterminer si chaque page est considéré comme un vrai PDF (exploitable sans ocr) ou un PDF scanné (une image convertie
en pdf).

Une fois analysé, la liste des pages des vrais PDF est envoyée grâce à la classe **"Send Request"** à l'application **"Extract Real PDF"** ainsi que le fichier PDF et la liste des pages des scans est envoyée à l'application **"Extract Scan
PDF"** ainsi que le fichier PDF. Les résultats sont ensuite stockés dans une liste. La liste des résultats est donc
envoyer à l'application **"Assembler Block"** pour être remis dans dans l'ordre initial grâce au numéro de page. Les
résultats sont des textes qui sont stockés dans une liste. Une classe **"Task Manager"** est utilisée pour gérer le
nombre de tâche qui sont traitées en même temps.

### Main steps

####  1. CheckType

To analyze type of input PDF file.

#### Input:
PDF file pages read by *pdfplumber*

#### Output :
A list of page number of scan pdf and real pdf

```agsl
type_pdf: {scan: [4,9], real_pdf: [0, 1, 2, 3, 5, 6, 7, 8, 10]}
```

Pour toutes les pages du document, on vérifie si une image est présente dans la page et on la compare avec la taille de
la page pour déterminer si c’est un scan ou pas. Si on trouve une image et que sa taille est supérieure ou égale à 90%
de la taille de la page OU que la taille de l’image est inférieure à 5 pixels (car des fichiers protégés convertissent
le texte en plusieurs pixels pour éviter la modification), alors, la page est considérée comme un scan et son numéro est
stocké dans un dictionnaire avec la clé "scan". Sinon, la page est un vrai pdf et son numéro est stocké dans le dictionnaire avec la clé "real_pdf".

#### 2. Send Request

Based on the results analyzed by **_CheckType_**, we will put the **_Extract Real PDF_** and **_Extract Scan PDF_** tasks into a list to obtain the final results of each page asynchronously.
#### Input:
* PDF file page number, example: 4 or 9
* PDF file pages read by *pdfplumber*

#### 3. Assemble Blocks

Put all the results in the correct order.

#### Input:
task_result

#### Output :
text by page



