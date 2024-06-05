# Segmentation

## Description

Cette application traite le segmentation de l'image d'une page du fichier PDF en plusieurs blocks d'image grâce à un modèle de détection d'objet. 

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
"Content-Type": "multipart/raw"

### Input:
Key: "file_name"
Value : image base 64

### Output :
JSON {"type de block(text,table,figure)" : {"image base 64" + bbox coordonnées}}


```
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

La fonction "handle_request" prend en entrée le nom de l'image ainsi que l'image en base 64 et retourne un JSON avec en clé le type du block et en valeur l'image du block en base 64. L'image en entrée est décodé puis convertie en Numpy Array pour être donnée à la fonction "predict". Ensuite, pour tous les éléments dans la sortie de la fonction précédente, les coordonnées des bounding box (bbox) sont stockées ainsi que les ID des types des bbox. Enfin, en fonction des ID, l'image, convertie en niveau de gris puis en base 64 par la fonction "grey_and_encode_base64", ainsi que ses coordonnées sont stockées dans une liste.

### predict

#### Input:
image

#### Output:
Result Model

La fonction "predict" va tout d'abord prédire le resultat de la détection des textes, tableaux et images présents sur la page. Le résultat va passer dans la fonction être trié en fonction des "y" puis envoyé à la fonction "clear_all_result" afin de garder seulement les bbox de text, tableau, image et graphe. Il sera ensuite envoyé à la fonction "reorder_image_list_with_xy".


### reorder_image_list_with_xy

La fonction "reorder_image_list_with_xy" prend en entrée le résultat de la prédiction trié en fonction des "y" et retourne une liste avec les résultats ordonnées en fonction des "x" et des "y". Tout d'abord, la valeur de la première détection sera stockée puis comparée grâce à la fonction "find_all_same_value_in_list" afin d'ordonner toute les bbox dans le bon sens de lecture. 

