# Extract Real PDF

### Description

This application handles the extraction of content from PDF file pages considered as “real PDF”.

### Library requirements

* json
* asyncio
* aiohttp
* sanic
* logging
* io
* hashlib
* base64
* random
* fitz
* pillow

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

/extract-real-pdf

#### port: 8014

#### Headers

"Content-Type": "multipart/form-data"

#### Input

Key: file  
Value: a PDF file

#### Output

a string list of content recognition

```json
[
    {
        "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—7b6f4703747ebe5debe54647754e89f86695d19b7c5792e7ba81956ac63af664—page0": [
            "R\nMissouri\nMissouri Small Business Facts\nMissouri's 121,350 small employers and\n394,913 nonemployers make significant 2007† 2006 2 0 00 contributions to the state's economy, and they Number of Businesses bring innovative products and services to the Small employers (<500 employees) n.a. 121,350 115,244 marketplace.* They are an important source of Large employers (500+ employees) n.a. 2,770 2,819\nNonemployers 394,913 380,499 311,786 employment and opportunity throughout the state. This profile by the Office of Advocacy 2002† % Share % Change in 2002 1997–2002 uses the latest statistics to describe the small\nBusiness Owner Demographics business contribution in the greatest possible\nMale-owned 236,814 53.9 15.5 detail. (Note: A small business is defined as one\nWoman-owned 120,443 27.4 16.2 with fewer than 500 employees.) Equally male/female-owned 67,963 15.5 -27.2\nAfrican American-owned 16,750 3.8 22.5\n• Missouri's real gross state product increased\nAsian-owned 6,376 1.5 31.9 by 1.3% and private-sector employment\nHispanic-owned 3,652 0.8 -11.1 decreased by 0.4% in 2008. By comparison, real Native American/Alaskan-owned 3,280 0.7 n.a.\nGDP growth in the United States was 0.7% and Hawaiian and Pacific Islander-owned 96 0.0 -31.4 private-sector employment declined by 0.7%. % Change from\n2008†\n• The health care and social assistance industry 2007 2000 was the state’s largest small business and overall Workforce (Thousands) /Unemployment (%) employer in 2006 (Table 1). Private-sector employment 2,285 -0.4 0.7\n• Small businesses are a major force in the Government employment 430 1.4 5.7 state's net job change, as shown in Table 2. Self-employed (incorp. & uninc.) 295 -8.1 15.5\nFemale self-employment 87 -23.5 15.1\n• The number of small employers in Missouri\nMale self-employment 208 0.2 15.7 was 121,350 in 2006, accounting for 97.8% of\nMinority self-employment 20 -24.5 22.7 the state's employers and 49.7% of its private- Veteran self-employment 36 -12.1 8.4 sector employment. (Source: U.S. Dept. of Unemployment rate (%) 6.1 1.0 2.8\nCommerce: Bureau of the Census.)\nBusiness Turnover\nQuarterly establishment openings 21,349 -1.8 -2.1\nFor Further Information\nQuarterly establishment closings 22,176 -4.9 -10.4\n• Data on all states and territories is available at\nBusiness bankruptcies 676 76.0 83.2 www.sba.gov/advo/research/profiles.\n2008† 2007 2000\n• For other small business data and analysis, visit www.sba.gov/advo/research, call (202) 205-6533, Income and Finance or email advocacy@sba.gov. Proprietors’ income ($billion) 16.0 15.5 11.8\n• Visit http://web.sba.gov/list to subscribe to Number of bank branches 2,427 2,376 2,096\nNo. of bus. loans under $100,000‡ n.a. 191,977 71,165 listservs for Advocacy’s newsletter, press releases,\nTotal value of business loans under regulatory news, and research reports. n.a. 1,946 995\n$100,000 ($million)‡\n• For RSS feeds, visit www.sba.gov/advo/ rsslibrary.html Source: U.S. Dept. of Commerce, Bureau of the Census and Bureau of Economic\nAnalysis; U.S. Dept. of Labor, Bureau of Labor Statistics; Administrative Office of the\n* Small employer data from 2006; nonemployer from 2007. U.S. Courts; Federal Deposit Insurance Corporation; and U.S. Small Business\nAdministration, Office of Advocacy (www.sba.gov/advo/research/sbl_08study.pdf,\nTable 4b.) n.a. not available.\n† Latest available data; certain figures are economywide. ‡Data are for CRA loans.\nSmall Business Profile: Missouri, Page 1 Published in October 2009 by the U.S. Small Business Administration, Office of Advocacy",
            "The image contains two key pieces of information:\n\n1. \"SBA Office of Advocacy\": This refers to the U.S. Small Business Administration's Office of Advocacy, which serves as the independent voice for small businesses within the federal government.\n\n2. \"Small Business Profile\": This appears to be the title of a publication or report focused on providing information and advocacy for small businesses.\n\nThe key relationship conveyed is that the SBA Office of Advocacy is responsible for producing the Small Business Profile, which likely contains data, analysis, and insights to support and represent the interests of small businesses in government policy and decision-making. The Office of Advocacy acts as the \"voice of small business in government\" as stated in the image.\n\nOverall, the image highlights the SBA Office of Advocacy's role in advocating for and providing a platform to amplify the concerns and perspectives of the small business community through publications and other initiatives."
        ]
    },
    {
        "R0Y0T0dFRDZESUZSNVdIQUJIVExTVEZWNzY1NkdLTjMucGRm—7b6f4703747ebe5debe54647754e89f86695d19b7c5792e7ba81956ac63af664—page1": [
            "Table 1. Firms and Employment in Missouri by Industry and Firm Size, 2006 and 2007\n(Nonfarm, Thousands)\nEmployer Firms (2006) Employment (2006)\nNonemployer 1-19 1-499 1-19 1-499\nIndustry Firms (2007) Total Employees Employees Total Employees Employees\nTotal 394.9 124.1 106.7 121.4 2,468.0 432.3 1,227.5\nForestry, etc. and agriculture support 5.3 0.3 0.2 0.3 1.6 (D) (D)\nMining 0.4 0.2 0.1 0.2 4.0 (D) (D)\nUtilities 0.3 0.1 0.1 0.1 16.3 0.3 3.3\nConstruction 59.9 16.9 15.4 16.8 154.6 61.4 130.6\nManufacturing 6.0 6.3 4.3 5.9 305.4 24.2 119.5\nWholesale trade 6.4 6.9 5.2 6.4 127.8 23.5 73.4\nRetail trade 40.9 15.2 13.0 14.7 326.5 59.9 138.5\nTransportation and warehousing 21.3 4.4 3.7 4.2 88.1 13.0 36.2\nInformation 4.6 1.4 1.0 1.2 69.5 4.5 16.2\nFinance and insurance 15.4 6.2 5.3 5.9 136.9 16.5 47.7\nReal estate and rental and leasing 43.0 5.6 5.1 5.5 42.5 13.6 28.5\nProfessional, scientific, and technical svcs. 43.1 12.9 11.6 12.6 137.9 39.6 84.8\nManagement of companies and enterprises -- 0.8 0.1 0.5 71.3 0.3 8.0\nAdmin., support, waste mgt., remed. svcs. 31.6 6.5 5.5 6.2 157.3 19.9 63.1\nEducational services 7.9 1.4 1.0 1.3 64.8 4.5 28.8\nHealth care and social assistance 28.6 12.0 10.0 11.8 362.9 47.6 171.0\nArts, entertainment, and recreation 17.9 2.0 1.7 2.0 38.0 6.7 23.2\nAccommodation and food services 4.8 9.0 6.6 8.8 239.8 37.4 146.7\nOther services (except public admin.) 57.7 15.1 13.9 15.0 120.6 56.0 102.3\nUnclassified -- 3.0 3.0 3.0 2.0 (D) 2.0\nSource: U.S. Dept. of Commerce, Bureau of the Census, Statistics of U.S. Businesses. (See www.sba.gov/advo/research/data.html for data from other years, and for starts, closures, job creation and destruction by industry and by size category.)\n(D) Data suppressed to protect the confidentiality of individual firms.\nTable 2: Net Job Change by Firm Size, 2003–2006 (Nonfarm)\nTotal Net Employment Size of Firm\nNew Jobs 1-4 5-9 10-19 20-99 100-499 <500 500+\n2003 - 2004 30,258 21,121 7,413 5,217 5,978 -750 38,979 -8,721\n2004 - 2005 11,032 16,687 2,152 -2,148 -7,853 -1,390 7,448 3,584\n2005 - 2006 43,552 15,632 3,713 7,641 3,380 272 30,638 12,914\nSource: U.S. Dept. of Commerce, Bureau of the Census. (For more detailed data see www.sba.gov/advo/research/data.html.)\nTable 3: Establishment and Employment Turnover by Quarter, 2008 (Nonfarm, Thousands)\nEstablishments Employment Change Due To:\nOpenings Expansions Contractions Closings Openings Expansions Contractions Closings\nQuarter 1 6.1 29.8 31.9 5.8 26.6 111.0 114.1 25.3\nQuarter 2 5.4 29.9 32.6 5.9 25.2 117.4 121.6 26.0\nQuarter 3 3.9 29.2 31.9 3.6 20.5 113.4 125.5 19.4\nQuarter 4 5.9 27.9 34.8 7.0 27.5 105.5 140.7 26.9\nSource: U.S. Dept. of Labor, Bureau of Labor Statistics, Business Employment Dynamics. (For more detailed data see www.bls.gov/bdm/home.htm.)\nNote: These figures contain all firm sizes; Census data from 2006 show that 86 percent of establishment births and deaths were in firms with fewer than 500 employees.\nSmall Business Profile: Missouri, Page 2 Published in Oct. 2009 by the U.S. Small Business Administration, Office of Advocacy"
        ]
    }
]
```

### Controller

![alt text](<Graph/Extract_real_pdf_graphe.png>)

The PDF file is sent to the **"Controller"** class along with the list of page numbers detected as "real PDF".

#### handle_request

The "handle_request" function takes the list of page numbers and the PDF file as input and returns the extraction result as output. The file name is converted to base 64 (to avoid errors due to spaces and special characters). A unique identifier is then assigned to the file name using the "generate_pdf_hash" function. For all the pages in the list, the file, page number, base 64 file name, and file ID are sent to the "handle_one_page" function. Finally, the results of this function are stored in a list.

#### handle_one_page

The "handle_one_page" function returns the extraction result for a single page. It first calls the "pdf_to_img_and_segmentation" function to segment the page into text blocks, tables, images, and graphics. If there are graphs present on the page, the previous elements are sent to the "ocr_correction_image_to_text" function. Otherwise, the elements are sent to the **"Extract Real PDF"** class. The result is stored in a list.

#### pdf_to_img_and_segmentation

The "pdf_to_img_and_segmentation" function takes the PDF file and the page number being processed as input. It returns the segmentation result. The PDF file is first converted to base 64 to be sent to the **"Convert PDF to Image"** application to convert the PDF pages into images. This allows for segmentation by sending the page image to the **"Segmentation Image to Blocks"** application.

#### ocr_and_correction_image_to_text

The "ocr_and_correction_image_to_text" function takes the resulting blocks from segmentation as input and returns a list of results. It performs content extraction from the pages based on the type of each block (text, table, image, graph). If it is text, the content is sent to the "ocr_and_correction" function. If it is a table, the content is sent to the **"OCR Table"** application. If it is an image or graph, the content is sent to the **"OCR Figure"** application. The image is also detected by the library PymuPDF. Then, all results are stored in a list.

#### ocr_and_correction

The "ocr_and_correction" function takes the name and content of the text block to be extracted as input and returns the extraction result. It first sends the input to the **"OCR Text"** application and then the result is sent to the **"Text Correction"** application. The corrected result is returned.

### Extract Real PDF

Pages that do not contain graphs are sent to the **"Extract Real PDF"** class to extract the content of the page.

#### extract_text

The "extract_text" function takes the page being processed, its name, and the table and image blocks resulting from segmentation as input. It returns a JSON with the page name as the key and the extraction result as the value. This function first extracts the texts. The content of the page is sent to the "deduplicate_text" function to extract the text and keep only once the words that were duplicated successively. It returns the texts in a list of strings. The list is sent to the "supprimer_sauts_de_ligne" function to maintain sentence continuity on the same line. The table blocks are sent to the **"OCR Table"** application and the image blocks are sent to the **"OCR Figure"** application. The results are then filtered to identify potential extraction errors based on the applications used. The filtered results are finally stored in a list and returned in JSON.

### Send Request

This class manages all functions that communicate with other applications. Here, it is used to communicate with the **"Convert PDF to Image"**, **"Segmentation Image to Blocks"**, **"OCR Text"**, **"OCR Figure"**, **"OCR Table"**, and **"Text Correction"** applications.
