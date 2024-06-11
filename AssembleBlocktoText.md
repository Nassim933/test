# Assemble

# Description

This application handles reordering the extraction result according to the original order of the PDF file.

## Library requirements

* re
* collections
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
/assemble-block-to-text

### port: 8007

### Headers :
"Content-Type": "application/json"

### Input:
JSON{"block name":"text result"}]

#### Example : 

```json
{"files":[
    {"bmFtZTEucGRm—9329abfe38bb504bc6280686bbdae4b3133689c18fa8d0ef46bc03318af5259b—page2—text—4":"Missouri's 721,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest possible detail. (Note: A small business is defined as one with fewer than 500 employees.)\n- Missouri's real gross state product increased by 1.3% and private-sector employment decreased by 0.4% in 2008. By comparison, real\nGDP growth in the United States was 0.7% and private-sector employment declined by 0.7%.\n- The health care and social assistance industry was the state’s largest small business and overall employer in 2006 (Table 1).\n- Small businesses are a major force in the state's net job change, as shown in Table 2.\n- The number of small employers in Missouri was 121,350 in 2006, accounting for 97.8% of the state's employers and 49.7% of its privatesector employment. (Source: U.S. Dept. of sector employment. (Source: U.S. Dept. of\nCommerce: Bureau of the Census.)\n"} , {"bmFtZTEucGRm—9329abfe38bb504bc6280686bbdae4b3133689c18fa8d0ef46bc03318af5259b—page1—text—3":"Missouri's 321,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest possible detail. (Note: A small business is defined as one with fewer than 500 employees.)\n- Missouri's real gross state product increased by 1.3% and private-sector employment decreased by 0.4% in 2008. By comparison, real\nGDP growth in the United States was 0.7% and private-sector employment declined by 0.7%.\n- The health care and social assistance industry was the state’s largest small business and overall employer in 2006 (Table 1).\n- Small businesses are a major force in the state's net job change, as shown in Table 2.\n- The number of small employers in Missouri was 121,350 in 2006, accounting for 97.8% of the state's employers and 49.7% of its privatesector employment. (Source: U.S. Dept. of sector employment. (Source: U.S. Dept. of\nCommerce: Bureau of the Census.)\n"}
    ]
}
```

### Output :
List of string


#### Example : 

```json
[
    "Missouri's 321,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest possible detail. (Note: A small business is defined as one with fewer than 500 employees.)\n- Missouri's real gross state product increased by 1.3% and private-sector employment decreased by 0.4% in 2008. By comparison, real\nGDP growth in the United States was 0.7% and private-sector employment declined by 0.7%.\n- The health care and social assistance industry was the state’s largest small business and overall employer in 2006 (Table 1).\n- Small businesses are a major force in the state's net job change, as shown in Table 2.\n- The number of small employers in Missouri was 121,350 in 2006, accounting for 97.8% of the state's employers and 49.7% of its privatesector employment. (Source: U.S. Dept. of sector employment. (Source: U.S. Dept. of\nCommerce: Bureau of the Census.)\n",
    "Missouri's 721,350 small employers and\n394,913 nonemployers make significant contributions to the state's economy, and they bring innovative products and services to the marketplace.* They are an important source of employment and opportunity throughout the state. This profile by the Office of Advocacy uses the latest statistics to describe the small business contribution in the greatest possible detail. (Note: A small business is defined as one with fewer than 500 employees.)\n- Missouri's real gross state product increased by 1.3% and private-sector employment decreased by 0.4% in 2008. By comparison, real\nGDP growth in the United States was 0.7% and private-sector employment declined by 0.7%.\n- The health care and social assistance industry was the state’s largest small business and overall employer in 2006 (Table 1).\n- Small businesses are a major force in the state's net job change, as shown in Table 2.\n- The number of small employers in Missouri was 121,350 in 2006, accounting for 97.8% of the state's employers and 49.7% of its privatesector employment. (Source: U.S. Dept. of sector employment. (Source: U.S. Dept. of\nCommerce: Bureau of the Census.)\n"
]
```

### assemble_blocks_to_text

The function "assemble_blocks_to_text" takes as input the name of the block along with its page number and its order on the page. For all the texts in the list, the page number and block number are stored in variables to first sort by pages and then by block numbers.