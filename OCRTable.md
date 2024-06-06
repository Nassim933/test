# OCR Table

### Description

This application extracts the image content of table blocks sent after segmentation.

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
/ocr_table

#### port: 8004

#### Headers :
"Content-Type": "application/json"

#### Input:
image base 64

#### Example:

```json
{
    "file_name" : "test",
    "file_content" : "JVBERi0xLjMKJcTl8uXrp/Og0MTGCjMgMCBvYmoKPDwgL0ZpbHRlciAvRmxhdGVEZWNvZGUgL0xlbmd0aCA2MCA+PgpzdHJlYW0KeAErVAhUKFTQD0gtSk4tKClNzFEoygQKmJpYKBgAobGZhYKxkYKRoZFCcq6CvmeuoYJLPlBLIAC+1Q6bCmVuZHN0cmVhbQplbmRvYmoKMSAwIG9iago8PCAvVHlwZSAvUGFnZSAvUGFyZW50IDIgMCBSIC9SZXNvdXJjZXMgNCAwIFIgL0NvbnRlbnRzIDMgMCBSIC9NZWRpYUJveCBbMCAwIDYxMiA3OTJdCj4"
}
```

#### Output :
a string of content recognition

#### Example:

```json
{
    "file_name": "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—5291c32235e6bbc6b2aeee0ad0ebb7d6bd69d234f1f740e2b95bcc366e541f58—page1—table–3",
    "result_ocr_tables": "Based on the information provided in the table, the following key details can be extracted:\n\nCurrent Assets:\n- Cash: $5,000\n- Accounts Receivable: $0\n- Pre-Opening Expenses: $250\n- Accounting: $500\n- Advertising: $500\n- Bank Charges: $350\n- Cable/Internet Services: $200\n- Insurance: $2,000\n- Ingredients: $3,500\n- Janitorial Supply: $75\n- Lease: $1,350\n- Legal Fees: $2,500\n- Licenses/Fees/Permits: $1,500\n- Payroll: $2,400\n- Payroll Taxes: $360\n- Telephone Services: $150\n- Utilities: $365\nTotal Current Assets: $15,500\n\nFixed Assets:\n- Kitchen Equipment: $9,000\n- Lease Hold Improvements: $18,200\n- Office/Tech Equipment: $2,300\nTotal Fixed Assets: $29,500\n\nTotal Assets: $50,000\n\nThe table provides a detailed breakdown of the current assets and fixed assets for the \"Year 1 Ope\" of \"The Wired Cup\" business. The total assets amount to $50,000, with $15,500 in current assets and $29,500 in fixed assets. The largest current asset items are Cash ($5,000), Ingredients ($3,500), and Lease ($1,350). The largest fixed asset items are Lease Hold Improvements ($18,200) and Kitchen Equipment ($9,000)."
}
```

The **"OCR Table ”** class takes the table block images as input, then Clause 3 extracts the text and returns the result as text.