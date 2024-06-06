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

The file is sent to the **"Controller"** class to be analyzed by the **"CheckType"** class in order to determine whether each page is considered a real PDF (processable without OCR) or a scanned PDF (an image converted to PDF).

Once analyzed, the list of real PDF pages is sent via the **"Send Request"** class to the **"ExtractRealPDF"** application along with the PDF file. The list of scanned pages is sent to the **"ExtractScanPDF"** application along with the PDF file. The results are then stored in a list. The list of results is sent to the **"AssemblerBlock"** application to be reordered according to the original page numbers. The results, which are texts, are stored in a list. A **"TaskManager"** class is used to manage the number of tasks being processed simultaneously.

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

For all the pages in the document, we check if an image is present on the page and compare its size with the size of the page to determine if it is a scan or not. If an image is found and its size is greater than or equal to 90% of the page size OR if the image size is less than 5 pixels (since protected files convert text into multiple pixels to prevent modification), then the page is considered a scan and its number is stored in a dictionary with the key "scan." Otherwise, the page is a real PDF and its number is stored in the dictionary with the key "real_pdf."

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



