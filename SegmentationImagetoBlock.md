# Segmentation

## Description

This application processes the segmentation of a PDF page image into several image blocks using an object detection model. 

## Library requirements

* cv2
* base64
* numpy
* ultralytics
* asyncio
* aiohttp
* sanic

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
python3 segmentation-image-to-block.py
```

or

```agsl
python segmentation-image-to-block.py
```

## Endpoint
/segment-image-to-block

### port: 8002

### Headers :
"Content-Type": "application/json"

### Input:
image base 64

#### Example:

```json
{
    "file_name" : "test",
    "file_content" : "JVBERi0xLjMKJcTl8uXrp/Og0MTGCjMgMCBvYmoKPDwgL0ZpbHRlciAvRmxhdGVEZWNvZGUgL0xlbmd0aCA2MCA+PgpzdHJlYW0KeAErVAhUKFTQD0gtSk4tKClNzFEoygQKmJpYKBgAobGZhYKxkYKRoZFCcq6CvmeuoYJLPlBLIAC+1Q6bCmVuZHN0cmVhbQplbmRvYmoKMSAwIG9iago8PCAvVHlwZSAvUGFnZSAvUGFyZW50IDIgMCBSIC9SZXNvdXJjZXMgNCAwIFIgL0NvbnRlbnRzIDMgMCBSIC9NZWRpYUJveCBbMCAwIDYxMiA3OTJdCj4"
}
```

### Output :
JSON {"type de block(text,table,figure)" : {"image base 64" + bbox coordonnées}}

#### Example:

```json
{
    "text_blocks": {
        "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—5291c32235e6bbc6b2aeee0ad0ebb7d6bd69d234f1f740e2b95bcc366e541f58—page1—text—1": [
            "iVBORw0KGgoAAAANSUhEUgAABdUAAAEYCAAfdsqfdsfdqf",
            [
                281,
                45,
                1574,
                125
            ]
        ],
        "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—5291c32235e6bbc6b2aeee0ad0ebb7d6bd69d234f1f740e2b95bcc366e541f58—page1—text—2": [
            "iVBORw0KGgoAAAANSUhEUgAAAtgAAAEMCAAAAADb/559AAAYi0lEQVR4Ae3BDXTU5b3g8e8zBpAQU14FgQmgRVRSZXJHr5Zi67vDXhntVWurVredzdQatcQpiJFWq+sKfYlVN7WttVfN/bdb5bBSq1LErn9TqfWlmoo4FkVRvCry0jAJkMQ8+3tmMskEOee296ihz/l9PsailH+MRSn/GItS/jEWpfxjLEr5x1iU8o+xKOUfY1HKP8ailH+MRSn/GItS/jEWpfxjLEr5x1iU8o+xKOUfY1HKP8ailH+MRSn/GItS/jEWpfxjLEr5x1iU8o+xKOUfY1H",
            [
                88,
                177,
                616,
                245
            ]
        ]
    },
    "table_blocks": {},
    "image_blocks": {
        "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—5291c32235e6bbc6b2aeee0ad0ebb7d6bd69d234f1f740e2b95bcc366e541f58—page1—figure—6": [
            "iVBORw0KGgoAAAANSUhEUgAAAmMAAAJlCAIAAAAZ82I3AAAgAElEQVR4AezBCZSe13kf9v9z733fb58VM4NtABIUJYIURYoitVGCBFm1ZSt2HS0mLdv1UhtpjtvUyW",
            [
                620,
                1369,
                1031,
                1782
            ]
        ]
    },
    "chart_blocks": {}
}
```

### handle_request

The "handle_request" function takes as input the image name and the base 64 encoded image, and returns a JSON with the block type as key and the block image in base 64 as value. The input image is decoded and then converted to a Numpy Array to be given to the "predict" function. Then, for all elements in the output of the previous function, the bounding box (bbox) coordinates are stored along with the bbox type IDs. Finally, based on the IDs, the image, converted to grayscale and then base 64 encoded by the "grey_and_encode_base64" function, along with its coordinates, are stored in a list.

### predict

#### Input:
image

#### Output:
Result Model

The "predict" function will first predict the result of detecting text, tables, and images present on the page. The result will pass through the function to be sorted according to "y" and then sent to the "clear_all_result" function to keep only the bbox of text, tables, images, and graphs. It will then be sent to the "reorder_image_list_with_xy" function.

### reorder_image_list_with_xy

The "reorder_image_list_with_xy" function takes as input the prediction result sorted according to "y" and returns a list with the results ordered according to "x" and "y". First, the value of the first detection will be stored and then compared using the "find_all_same_value_in_list" function to order all the bboxes in the correct reading direction.


