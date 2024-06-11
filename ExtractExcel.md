# Extract Excel

### Description

This application is used to extract content from Excel files.

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

The "extract_excel" function takes the Excel file as input and returns the extraction result.

First, we open the file using the _openpyxl_ library. For each sheet in the workbook, if the sheet is not empty (checked using the "is_sheet_empty" function), we convert the sheet elements to CSV using the "sheet_to_csv_string" function. Then, we clean the sheet by deleting empty rows at the beginning with the "delete_void_line_in_front_of_sheet" function and by deleting all empty columns with the "delete_all_blank_columns" function. We then calculate the number of tokens using the "count_tokens" function from the **"Token Calculator"** class to compare it to the predefined maximum number of tokens. If the sheet's token count is below the max token count, the CSV is sent to the "generate_message_content" function (without a previous message) to generate the expected structure for the **"CSV Interpreter"** application, which provides a detailed explanation of the sheet. If the max token count is exceeded, the sheet is sent to the "extract_long_sheet_page" function.

If there are images in the file, they are sent to the **"OCR Figure"** application.

If the result type is a list (result from the "extract_long_sheet_page" function), it is directly added to the final result list. Otherwise, we use the "find_value_in_dict" function to retrieve the results from CSV Interpreter and OCR Figure, which will be in a dictionary if the file was not split.

#### extract_long_sheet_page

The "extract_long_sheet_page" function takes a CSV file sheet and its index as input and returns the result in a list and the index.

First, we split the sheet based on completely empty lines using the "split_with_empty_line" function. Then, the split CSV is sent to the "split_everything_with_max_token" function to separate the sheet based on the predefined maximum number of tokens.

For each element in the split sheet list, the "generate_message_content" function is applied, but this time with the previous message to maintain the file context and not lose the meaning.

The result and the page index are sent to the **"CSV Interpreter"** application. The result is then sent to the "find_value_in_dict" function and returned as a list with the page index.

#### split_everything_with_max_token

The "split_everything_with_max_token" function takes the list with split elements of the Excel sheet based on empty lines and the maximum number of tokens as input. It returns a list with elements split based on the number of tokens.

First, we calculate the number of tokens for each element in the list. If an element exceeds the max token count, it is recursively sent to the "split_everything_with_max_token" function with the element split based on line breaks, as the input type is a list.

If the token count of the element is within the limit, it is added to the result list.

#### generate_message_content

The "generate_message_content" function takes the CSV content and the previous messages as input. It returns the previous message plus the new message.

This function structures the message to be sent to the **"CSV Interpreter"** application and maintains the sheet context. The previous message and the new message are sent to **"CSV Interpreter"** so that Claude 3 can have the context (header, legend...) and provide the best explanation of the elements.
