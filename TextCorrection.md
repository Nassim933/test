# Text Correction

# Description

This application takes care of correcting spelling errors in the output of the **"OCR Text ”** application.

## Library requirements

* langdetect
* spellchecker
* logging
* asyncio
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
python3 app.py
```

or

```agsl
python app.py
```

## Endpoint
/text-correction

### port: 8006

### Headers :
"Content-Type": "application/json"

### Input:
JSON of text result

#### Example:

```json
{
    "file_name" : "test",
    "file_content" : "Missouri's 721,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest "
}
```

### Output :
JSON of correction result

#### Example:

```json
{
    "file_name": "test",
    "result_correction": "Missouri's 721,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest "
}
```

### correct_text

The "correct_text" function takes the text to be corrected as input. First, we will detect the language to choose the appropriate dictionary for text correction. We have dictionaries for English, French, German, and Spanish. If the detected language is in this list, the dictionary will be selected using the "load_dictionary" function. Then, the text will go through the "spelling_correction" function and return the corrected text. Otherwise, the original text will be returned.

### spelling_correction

The "spelling_correction" function takes the text and the dictionary corresponding to the text's language as input. It will first convert the text into a list of strings. Then, for each element in the list and for all words that start with a lowercase letter, if the word is present in the dictionary, it is considered correctly spelled. Otherwise, it is corrected using the _spellchecker_ library.
