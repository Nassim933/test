# CSV Interpreter

### Description

This application interprets the contents of a CSV.

### Library requirements

* sanic
* logging
* asyncio
* aiohttp
* inspect

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

/csv_interpreter

#### port: 8012

#### Headers

"Content-Type": "multipart/form-data"

#### Input
JSON with en dictionary with the keys "role"(user or assistant) and "content". 

```json
{
    "message_content":[{"role": "user",
                               "content": "[Nom de l’entreprise];;;;;;FACTURE;\n[Rue];;;;;;;\n[Code postal, Ville];;;;;;;\nTéléphone : 06 12 34 56 78;;;;;N° FACTURE;;DATE\n;;;;;2034;;2018-02-21 00:00:00\n;;;;;;;\nFACTURER À;;;;;RÉF CLIENT;;CONDITIONS\n[Nom];;;;;564;;Paiement dû à la réception\n[Nom de l’entreprise];;;;;;;\n[Rue];;;;;;;\n[Code postal, Ville];;;;;;;\n[Téléphone];;;;;;;\n[Adresse e-mail];;;;;;;\n;;;;;;;\nDESCRIPTION;;;;;QTÉ;PRIX UNITAIRE;MONTANT\nFrais de service;;;;;1;200;200\nMain-d’œuvre : 5 heures à 75 €/h;;;;;5;75;375\nRemise nouveau client;;;;;;-50;-50\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\n;;;;;;;0\nNous vous remercions de votre confiance.;;;;;SOUS-TOTAL;;525\n;;;;;TAUX TVA;;0.0425\n;;;;;TAXE;;22.3125\n;;;;;TOTAL;;547.3125\n;;;;;;;\n;;;;;;;\nPour toute question concernant cette facture, veuillez contacter;;;;;;;\n[Nom, téléphone, email@adresse.com];;;;;;;"}]
 
}
```

#### Output

JSON with String of result 

```json
{
    "result_csv_interpreter": "[Nom de l'entreprise]\n[Rue]\n[Code postal, Ville]\nTéléphone : 06 12 34 56 78\n\nFACTURE\nN° FACTURE : 2034\nDATE : 2018-02-21 00:00:00\n\nFACTURER À\n[Nom]\n[Nom de l'entreprise]\n[Rue]\n[Code postal, Ville]\n[Téléphone]\n[Adresse e-mail]\n\nRÉF CLIENT : 564\nCONDITIONS : Paiement dû à la réception\n\nDESCRIPTION    QTÉ    PRIX UNITAIRE    MONTANT\nFrais de service    1    200    200\nMain-d'œuvre : 5 heures à 75 €/h    5    75    375\nRemise nouveau client    -    -50    -50\n\nSOUS-TOTAL : 525\nTAUX TVA : 0.0425\nTAXE : 22.3125\nTOTAL : 547.3125\n\nNous vous remercions de votre confiance.\n\nPour toute question concernant cette facture, veuillez contacter\n[Nom, téléphone, email@adresse.com]"
}

```

The **"CSV Interpreter "** class takes the CSV content as input, so that Claude 3 can extract the information. 