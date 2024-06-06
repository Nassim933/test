# OCR Text

### Description

This application extracts image content from text blocks sent after segmentation.

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
    "file_name": "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—5291c32235e6bbc6b2aeee0ad0ebb7d6bd69d234f1f740e2b95bcc366e541f58—page1—3",
    "ocr_text_result": "Missouri's 121,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest possible detail. (Note: A small business is defined as one with fewer than 500 employees.)\n- Missouri's real gross state product increased by 1.3% and private-sector employment decreased by 0.4% in 2008. By comparison, real\nGDP growth in the United States was 0.7% and private-sector employment declined by 0.7%.\n- The health care and social assistance industry was the state’s largest small business and overall employer in 2006 (Table 1).\n- Small businesses are a major force in the state's net job change, as shown in Table 2.\n- The number of small employers in Missouri was 121,350 in 2006, accounting for 97.8% of the state's employers and 49.7% of its privatesector employment. (Source: U.S. Dept. of sector employment. (Source: U.S. Dept. of\nCommerce: Bureau of the Census.)\n"
}
```

The **"OCR Text ”** class takes text block images as input, then Clause 3 extracts the text and returns the result as text.