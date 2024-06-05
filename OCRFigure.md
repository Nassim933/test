# OCR Figure

### Description

Cette application permet d'extraire le contenu des images des blocks d'image ou de graphe envoyées après la segmentation.

### Library requirements

* asyncio
* aiohttp
* sanic
* logging
* inspect
* numpy
* opencv
* pytesseract
* pillow
* random
* re

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
/ocr_figure

#### port: 8005

#### Headers :
"Content-Type": "application/json"

#### Input:
Key: file_name  
Value: image base 64

#### Output :
a string of content recognition

```
{
    "file_name": "RTdPNE1DSUpHSktKU1oyRzNJRDJIUEpNSEtLUUVTT04ucGRm—acd3c9107f7f3b51494a7a8dd8309826db6240bc956c2ce5a988de21081b2df5—page1—figure—13",
    "result_ocr_figure": "The image appears to be an advertisement or promotional material for a company called \"Projecteurs\" that specializes in lighting solutions for interior architecture projects. The main text prominently displays the phrase \"SE LANCER DANS L'ARCHITECTURE D'INTERIEUR\" which translates to \"Get started in interior architecture\".\n\nThe image depicts two people, a man and a woman, working on an interior design project using various tools and equipment. The man is shown standing on a ladder, likely projecting or displaying something, while the woman is seated at a desk, presumably working on plans or designs.\n\nThe image also includes the logos of two companies, \"BPI France\" and \"Création\", which are likely partners or sponsors of the Projecteurs company. 1. The company \"Projecteurs\" specializes in lighting solutions for interior architecture projects.\n2. The main text encourages people to \"Get started in interior architecture\".\n3. The image depicts two people, a man and a woman, working on an interior design project.\n4. The man is standing on a ladder, likely projecting or displaying something.\n5. The woman is seated at a desk, presumably working on plans or designs.\n6. The image includes the logos of two companies, \"BPI France\" and \"Création\", which are likely partners or sponsors of Projecteurs. The knowledge extraction task for this image was relatively straightforward, as the image clearly conveys information about the Projecteurs company and its focus on interior architecture projects. The visual elements, such as the people working on the project and the tools and equipment they are using, provide clear and specific details that can be extracted as knowledge. The inclusion of the partner company logos also provides additional context about the image. Overall, the image is well-designed and communicates its message effectively, making the knowledge extraction process relatively easy."
}
```

La classe **"OCR Figure"** prend en entrée les images des blocks d'image ou de graphe, puis l'image est envoyé à la fonction "check_ocr_text". Ensuite, Clause 3 s'occupe d'extraire une explication du contenu de l'image et retourne liste avec le résultat. Cette liste est ensuite traitée dans la fonction "extract_usable_knowledge" afin d'en extraire seulement le contenu utile.

#### check_ocr_text

La fonction "check_ocr_text" prend en entrée l'image en base 64 et retourne un booléen. Cette fonction nous sert à voir s'il est utilise d'exploiter le contenu de cette image. Pour cela, nous effectuons de l'OCR sur l'image avec Tesseract. Si l'OCR donne un resultat, alors nous envoyons l'image à Claude 3. Sinon, l'image n'est pas traitée. 
