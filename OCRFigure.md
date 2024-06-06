# OCR Figure

### Description

This application extracts image content from image blocks or graphs sent after segmentation.

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
image base 64

#### Example : 

```json
{
    "file_name" : "test",
    "file_content" : "JVBERi0xLjMKJcTl8uXrp/Og0MTGCjMgMCBvYmoKPDwgL0ZpbHRlciAvRmxhdGVEZWNvZGUgL0xlbmd0aCA2MCA+PgpzdHJlYW0KeAErVAhUKFTQD0gtSk4tKClNzFEoygQKmJpYKBgAobGZhYKxkYKRoZFCcq6CvmeuoYJLPlBLIAC+1Q6bCmVuZHN0cmVhbQplbmRvYmoKMSAwIG9iago8PCAvVHlwZSAvUGFnZSAvUGFyZW50IDIgMCBSIC9SZXNvdXJjZXMgNCAwIFIgL0NvbnRlbnRzIDMgMCBSIC9NZWRpYUJveCBbMCAwIDYxMiA3OTJdCj4"
}
```

#### Output :
a string of content recognition

#### Example : 

```json
{
    "file_name": "RTdPNE1DSUpHSktKU1oyRzNJRDJIUEpNSEtLUUVTT04ucGRm—acd3c9107f7f3b51494a7a8dd8309826db6240bc956c2ce5a988de21081b2df5—page1—figure—13",
    "result_ocr_figure": "The image appears to be an advertisement or promotional material for a company called \"Projecteurs\" that specializes in lighting solutions for interior architecture projects. The main text prominently displays the phrase \"SE LANCER DANS L'ARCHITECTURE D'INTERIEUR\" which translates to \"Get started in interior architecture\".\n\nThe image depicts two people, a man and a woman, working on an interior design project using various tools and equipment. The man is shown standing on a ladder, likely projecting or displaying something, while the woman is seated at a desk, presumably working on plans or designs.\n\nThe image also includes the logos of two companies, \"BPI France\" and \"Création\", which are likely partners or sponsors of the Projecteurs company. 1. The company \"Projecteurs\" specializes in lighting solutions for interior architecture projects.\n2. The main text encourages people to \"Get started in interior architecture\".\n3. The image depicts two people, a man and a woman, working on an interior design project.\n4. The man is standing on a ladder, likely projecting or displaying something.\n5. The woman is seated at a desk, presumably working on plans or designs.\n6. The image includes the logos of two companies, \"BPI France\" and \"Création\", which are likely partners or sponsors of Projecteurs. The knowledge extraction task for this image was relatively straightforward, as the image clearly conveys information about the Projecteurs company and its focus on interior architecture projects. The visual elements, such as the people working on the project and the tools and equipment they are using, provide clear and specific details that can be extracted as knowledge. The inclusion of the partner company logos also provides additional context about the image. Overall, the image is well-designed and communicates its message effectively, making the knowledge extraction process relatively easy."
}
```

The **"OCR Figure"** class takes as input the images of image or graph blocks, and then the image is sent to the "check_ocr_text" function. Then, Clause 3 is responsible for extracting an explanation of the image content and returns a list with the result. This list is then processed in the "extract_usable_knowledge" function to extract only the useful content.

#### check_ocr_text

The "check_ocr_text" function takes the base 64 encoded image as input and returns a boolean. This function is used to determine if it is useful to exploit the content of this image. To do this, we perform OCR on the image using Tesseract. If the OCR yields a result, then we send the image to Clause 3. Otherwise, the image is not processed.
