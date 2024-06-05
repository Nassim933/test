# OCR Text

### Description

Cette application permet d'extraire le contenu des images des blocks textes envoyées après la segmentation.

### Library requirements

* asyncio
* aiohttp
* sanic
* logging
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
/ocr_text

#### port: 8003

#### Headers :
"Content-Type": "application/json"

#### Input:
Key: file_name  
Value: image base 64

#### Output :
a string of content recognition

La classe **"OCR Text"** prend en entrée les images des blocks textes, puis Clause 3 s'occupe d'extraire le texte et retourne le resultat en texte.