# Extract PPTX

### Description

This application is used to extract content from PowerPoint files.

### Library requirements

* sanic
* logging
* asyncio
* io
* aiohttp
* base64
* random
* inspect
* pptx
* os
* xml
* lxml
* datetime

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

/extract-pptx

#### port: 8009

#### Headers

"Content-Type": "multipart/form-data"

#### Error Code

500 : Error in form data  
415 : Format not allowed or unsupported

#### Input

Key: file  
Value: a PPTX file

#### Output

JSON with the file name and a string list of content recognition

```json
{
    "file_name": "Etude-de-marche-mars-2022-vf.pptx",
    "result_extract_ppt": [
        "This slide discusses the importance of conducting market research to gather information about the market environment, customers, and competitors in order to determine the market trends, target customer segments, sales approach, and projected revenue.\n\nThe slide outlines three key areas to research:\n1. The market environment - This involves understanding the overall state","This slide outlines the key elements that make up the environment in which a product or service operates. The slide lists several different types of stakeholders or \"intervenants\" that are involved in this environment:\n\n\"Offre\" (Supply) - This refers to the producers or suppliers of the product or service.\n\"Demande\" (Demand) - This refers to the consumers or customers who are the end users of the product or service.\n\"Distributeurs\" (Distributors) - These are the intermediaries who help get the product or service from the producers to the consumers.\n\"Pr"]
}
```
![alt text](<Graph/ExtractPPTX_graph.png>)

#### extract_text_from_pptx

The "extract_text_from_pptx" function takes the PowerPoint file and the file name as input if it is in PPTX format and returns the extraction result.

Each slide is processed by the "extract_one_page" function. This allows multiple slides to be processed simultaneously. The results are then added to a list of strings.

#### extract_one_page

The "extract_one_page" function takes the file name, the slide being processed, and its index as input. It returns a string with the extraction result of the slide.

For each element on the slide, depending on the type of element, the "extract_text_from_different_type" function is applied to extract the content of each type of element. Then, we check for any tabulation issues instead of line breaks with the "tab_to_jump" function. The result is sent to the "recompose_slide_information" function to reorder the slide elements to maintain reading flow.

#### extract_text_from_different_type

The "extract_text_from_different_type" function takes the element to be processed, the slide, the file name, and its index as input. It returns the text of the relevant element.

For elements of type "text" (type number: 17, 5, 1) that are not empty, we retrieve the text with the "recover_text" function, which extracts and returns the text.

For elements of type "placeholder" (object text or image)(14), we first check if it is text (1, 2, 3, 15, 4) or an image (7, 16). For images, we retrieve the content with the "ocr_image" function, which converts the image to base 64 and sends it to the **"OCR Figure"** application. For text, the element is sent to the "recover_text" function.

For elements of type "image" (13), they are sent to the "ocr_image" function.

For elements of type "table" (19), they are sent to the "recover_data_table" function.

For elements of type "smart art" (GraphicFrame), they are sent to the "recorver_data_smart_art" function.

For elements of type "chart" (3), they are sent to the "recover_data_chart" function.

#### recompose_slide_information

The "recompose_slide_information" function takes the slide text as input and returns the ordered text. The input is processed by Claude 3 to manage the reordering of slide elements.

#### recover_data_table

The "recover_data_table" function takes elements of type "table" as input and returns the content in CSV format.

We loop through the columns of each row, retrieve the text from each cell, and add a ';' as a separator.

#### recorver_data_smart_art

The "recorver_data_smart_art" function takes elements of type "smart art" and the slide as input. It returns the text content of the smart art.

We retrieve the content using the slide's XML with the "diagram" namespace.

#### recover_data_chart

The "recover_data_chart" function takes elements of type "chart" and the slide as input and returns the result in CSV format.

We retrieve all chart elements with the namespace "/drawingml/2006/chart" and if we find the "chart" relation, we retrieve the following information from the chart: ```{"title": "", "categories": [], "data": []}```. We check with the "is_date_format" function if there is a date in the chart and if it is in the correct format. If it is not in the correct format, the date will be formatted correctly using the "excel_date_to_datetime" function. The data from the table is retrieved with the './/c:ser' tag for series. The chart information is then formatted as CSV using the "json_to_csv" function.

