# Extract Real PDF

### Description

Cette application traite l'extraction du contenu des pages du fichier PDF considérées comme "vrai PDF".

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

```
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

Le fichier PDF est envoyé à la classe **"Controller"** ainsi que la liste des numéros des pages détéctées comme "vrai PDF".

#### handle_request

La fonction "handle_request" prend en entrée la liste des numéros de page et le fichier PDF et retourne en sortie le résultat de l'extraction du contenue. Le nom du fichier est convertie en base 64 (pour éviter les erreurs à cause des espaces et des caractères spéciaux). On va ensuite attribuer un identifiant unique au nom du fichier avec la fonction "generate_pdf_hash". Pour toutes les pages qui se trouvent dans la liste, on envoie le fichier, le numéro de page, le nom du fichier en base 64 et l'ID du fichier à la fonction "handle_one_page".Enfin, les résulats de cette fonction seront stockés dans une liste.

#### handle_one_page

La fonction "handle_one_page" retourne le résultat de l'extraction pour une seul page. Elle va tout d'abord appeler la fonction "pdf_to_img_and_segmentation" afin de segmenter la page en blocks de textes, tableaux, images et graphiques. S'il y a des graphes présents dans la page, les éléments précédents sont envoyés à la fonction "ocr_correction_image_to_texte". Sinon, les éléments sont envoyés à la classe **_"Exctract Real PDF"_**. Le résultat est stocké dans une liste.

#### pdf_to_img_and_segmentation

La fonction "pdf_to_img_and_segmentation" prend en entrée le fichier PDF et le numéro de la page qui est en cours de traitement. Elle retourne le résultat de la segementation. Le fichier PDF sera tout d'abord convertie en base 64 pour être envoyé à l'application **"Convert PDF to Image"** afin de convertir les pages du PDF en images. Cela permettra d'effectuer la segmentation en envoyant l'images de la page à l'application **"Segmentation Image to Blocks"**.

#### ocr_and_correction_image_to_texte

La fonction "ocr_and_correction_image_to_texte" prend en entrée les blocks résultants de la segmentation et retourne une liste des résultats. Elle permet d'effectuer l'extraction du contenu des pages en fonctions du type de chaque block (texte, tableau, image, graphe). Si c'est un texte, le contenu est envoyé à la fonction "ocr_and_correction". Si c'est un tableau, le contenu est envoyé à l'application **"OCR Table"**. Si c'est une image ou un graphe, le contenu est envoyé à l'application **"OCR Figure"**. Ensuite, tous les résultats sont stockés dans une liste.

#### ocr_and_correction

La fonction "ocr_and_correction" prend en entrée le nom et le contenu du block de texte à extraire et retourne le résultat de l'extraction. Elle va tout d'abord envoyer l'entrée à l'application **"OCR Text"** et ensuite, le résultat sera envoyé à l'application **"Text Correction"**. C'est donc le resultat de la correction qui sera retourné.

### Extract Real PDF

Les pages qui ne contiennent pas de graphes sont envoyées à la classe **"Extract Real PDF"** pour extraire le contenu de la page.

#### extract_text

La fonction "extract_text" prend entrée la page en cours de traitement, son nom ainsi que les blocks de tableau et d'image résultant de la segmentation. Elle retourne un JSON avec le nom de la page en clé et le résultat de l'extraction en valeur. Cette fonction va extraire tout d'abord les textes. Pour cela, on va envoyer le contenu de la page à la fonction "deduplicate_text" afin d'extraire le texte de la page et de garder seulement une fois les mots qui se sont dupliqués successivement. Elle retournera les textes dans une liste de string. La liste est envoyée à la fonction "supprimer_sauts_de_ligne" afin de garder la continuité des phrases sur la même ligne. Les blocks de tableau sont envoyés à l'application **"OCR Table"** et les blocks d'image sont envoyés à l'application **"OCR Figure"**. Ensuite, les résultats sont filtrés pour remonter les potentielles erreurs d'extraction en fonction des applications utilisées. Les résultats filtrés sont enfin stockés dans une liste puis retournés en JSON.

### Send Request

Cette classe permet de gérer toutes les fonctions qui commnuniquent avec d'autres applications. Ici, on l'utilise pour communiquer avec les applications **"Convert PDF to Image"**, **"Segmentation Image to Blocks"**, **"OCR Text"**, **"OCR Figure"**, **"OCR Table"** et **"Text Correction"**.
