# PDF to Image

## Description

This application converts each page of a PDF file into an image.

## Library requirements

* sanic
* io
* base64
* hashlib
* pdfplumber

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

## Endpoint
/convert

### port: 8001

### Headers :
"Content-Type": "application/json"

### Input:
PDF base 64 + page list

#### Example:

```json
{
    "file_name" : "test",
    "page_list" : [1,2,3],
    "file_content": "JVBERi0xLjIKJbHPquK6DQogICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgCnhyZWYKMiA0IAowMDAwMDAwMzY2IDAwMDAwIG4NCjAwMDAwMDA0MjAgMDAwMDAgbg0KMDAwMDAwMDYyMiAwMDAwMCBuDQowMDAwMDAwNjk5IDAwMDAwIG4NCnRyYWlsZXIKPDwgCi9TaXplIDY0IAovSURbPDMzMEEyODA3RTc0RTAxRTJERDYwMUM4RUY2OUE0QzQwPjwzMzBBMjgwN0U3NEUwMUUyREQ2MDFDOEVGNjlBNEM0MD5dCi9Sb290IDIgMCBSIAovSW5mbyA2MyAwIFIgCi9QcmV2IDYyNjg3MjAgCj4"
}
```

### Output :
image base 64 + total page number

#### Example:

```json
{
    "images": {
        "dGVzdA==—3d18b477f102ee4e826d01b1a1519bbf189feba3a91defc82ccf6e60712a9333—page1": "iVBORw0KGgoAAAANSUhEUgAACbAAAA25CAMAAACl/BrhAAADAFBMVEVZYtvfV2iWo91YZabrmqgdIyBaZF7q39pvktUxVFU1Xq6ZoqJvjaCuy+TmcosjKFIsRzDcttpMLSxOTjcvLak6VMmNjneRZmhthm7cOVM2N8qEeuLTz7hUN1StxbCSd5hFOqtDO86eNU2aLTY1hHLXMTs4iIbQQzruhXo9gcqMRzh3yI5twvv+/"
        },
    "total_pages": 20
}
```

### generate_pdf_hash

The "generate_pdf_hash" function generates a unique identifier for each PDF in case two PDFs have the same name.

### convert_pdf_to_images

The "convert_pdf_to_images" function will first decode the base 64 encoded PDF and then open it with *pdf_plumber*. Each page in the input list will be converted to an image with 300 DPI and then converted to base 64.
