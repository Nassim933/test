# Exctract Word

### Description

This application is used to extract content from Word files.

### Library requirements

* sanic
* logging
* asyncio
* io
* aiohttp
* base64
* random
* inspect
* docx
* os
* xml
* datetime
* math
* doc2pdf

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

/extract-word

#### port: 8010

#### Headers

"Content-Type": "multipart/form-data"

#### Error Code

500 : Error in form data  
400 : No file provided  
415 : Format not allowed or unsupported  

#### Input

Key: file  
Value: a DOCX or DOC file

#### Output

JSON with the file name and a string list of content recognition

```json
{
    "file_name": "Copie de fiche évaluation de la période en entreprise.docx",
    "result_extract_word": [
        "FICHE D'EVALUATION DE L’ETUDIANT LORS DE SA PERIODE EN ENTREPRISE",
        "A rattacher à votre rapport de stage, ",
        "EFREI - 30/32, avenue de la République - 94800 VILLEJUIF",
        "NOM de l’étudiant : \t Prénom : \t",
        "Promotion de l’étudiant : ……………",
        "Dates du stage : \t",
        "ENTREPRISE (Nom et adresse) : \t",
        "Nom du représentant de l’entreprise : \t",
        " : \t @ : \t",
        "Poste occupé durant le stage :",
        "DEFINITION DU TRAVAIL EFFECTUE",
        "CRITERES D’EVALUATION :",
        "APPRECIATION GENERALE (points forts et points faibles du stagiaire) :",
        "Cette évaluation a-t-elle été discutée avec le stagiaire ?      oui /      non ",
        "Seriez-vous disposé à recevoir un autre étudiant du groupe Efrei ?     oui /     non",
        "Date :\t\t\t Cachet de l'entreprise :\t\t\tSignature :",
        "\t\t\t\t\t (obligatoire)\t\t\t\t\t"
    ]
}
```

![alt text](<Graph/ExtractWord_graph.png>)

#### extract_text_from_docx

The "extract_text_from_docx" function takes the Word file as input if it is in DOCX format and returns the extraction result.

First, the file is opened using the "docx" library. Then, for all elements in the file, using the XML tags, we detect tables, text, images, catalogs, charts, and smart art.

For tables (tag 'tbl'), we loop through the columns of each row, retrieve the text from each cell, and add a ';' as a separator. Then, we calculate the number of tokens in the result using the **"TokenCalculator"** class and compare it with the specified maximum number of tokens. If it is less than the max tokens, the result is sent to the "interpretation" function, which sends it to the **"Interpreter CSV"** application. Otherwise, it is sent to the "split_table" function, and each split element is sent to the "interpretation" function.

For text (tag 'p'), we retrieve the value based on the "namespace" and add it to a list of strings.

For catalogs (tag 'sdt'), we retrieve the elements using the 'hypertext' tag.

For images (tag 'pic'), depending on the namespace, if we find the "image" relation in the types of relation, the retrieved image is converted to base 64 to be sent to the **"OCR Figure"** application.

For charts (tag 'chart'), we retrieve all chart elements with the namespace "/drawingml/2006/chart" and if we find the "chart" relation, we retrieve the following information from the chart: ```{"title": "", "categories": [], "data": []}```. We check with the "is_date_format" function if there is a date in the chart and if it is in the correct format. If it is not in the correct format, the date will be formatted correctly using the "excel_date_to_datetime" function. The data from the table is retrieved with the './/c:ser' tag for series. The chart information is then formatted as CSV using the "json_to_csv" function to be sent to the **"Interpreter CSV"** application.

For Smart Art (tag 'diagram'), we retrieve all graphic elements with the namespace "/drawingml/2006/diagram" and if we find the "diagramData" relation, we retrieve all the content.

All the results in the 'extracted_text' string list are sent to the "clean_extracted_text" function.

If an error occurs during the extraction of any part, the file is converted to PDF and sent to the **"Extract PDF"** application.

#### clean_extracted_text

The "clean_extracted_text" function takes the extraction result as input and returns the text with line breaks removed.

#### split_table

The "split_table" function intelligently splits the table to respect the number of tokens without losing the table's meaning. It is first split by empty lines using the "split_with_empty_line" function. Then, for each element of the split, we remove empty columns with the "delete_all_blank_columns" function. We find the header with the "find_header" function to keep it for all elements. Finally, each element is split based on the maximum number of tokens allowed per element with the "split_per_number_of_token" function.

#### extract_text_from_doc

The "extract_text_from_docx" function takes the Word file as input if it is in DOC format and returns the extraction result.

It will convert the file to PDF and send it to the **"Extract PDF ”** application.
