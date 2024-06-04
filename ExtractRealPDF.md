# Extract Real PDF

## Entrée :  PDF file + liste des numéros de page

## Sortie : Liste de String

Cette application traite l'extraction du contenu des pages du fichier PDF considérées comme "vraie PDF".

### Controller 

Le fichier PDF est envoyé à la classe **"Controller"** ainsi que la liste des numéros des pages détéctées comme "vraie PDF". 

La fonction "handle_request" prend en entrée la liste des numéros de page et le fichier PDF et retourne en sortie le résultat de l'extraction du contenue. Le nom du fichier est convertie en base 64 (pour éviter les erreurs à cause des espaces et des caractères spéciaux). On va ensuite attribuer un identifiant unique au nom du fichier avec la fonction "generate_pdf_hash". Pour toutes les pages qui se trouvent dans la liste, on envoie le fichier, le numéro de page, le nom du fichier en base 64 et l'ID du fichier à la fonction "handle_one_page".Enfin, les résulats de cette fonction seront stockés dans une liste. 

La fonction "handle_one_page" retourne le résultat de l'extraction pour une seul page. Elle va tout d'abord appeler la fonction "pdf_to_img_and_segmentation" afin de segmenter la page en blocks de textes, tableaux, images et graphiques. S'il y a des graphes présents dans la page, les éléments précédents sont envoyés à la fonction "ocr_correction_image_to_texte". Sinon, les éléments sont envoyés à la classe **"Exctract Real PDF"**. Le résultat est stocké dans une liste.

La fonction "pdf_to_img_and_segmentation" prend en entrée le fichier PDF et le numéro de la page qui est en cours de traitement. Elle retourne le résultat de la segementation. Le fichier PDF sera tout d'abord convertie en base 64 pour être envoyé à l'application **"Convert PDF to Image"** afin de convertir les pages du PDF en images. Cela permettra d'effectuer la segmentation en envoyant l'images de la page à l'application **"Segmentation Image to Blocks"**. 

La fonction "ocr_and_correction_image_to_texte" prend en entrée les blocks résultants de la segmentation et retourne une liste des résultats. Elle permet d'effectuer l'extraction du contenu des pages en fonctions du type de chaque block (texte, tableau, image, graphe). Si c'est un texte, le contenu est envoyé à la fonction "ocr_and_correction". Si c'est un tableau, le contenu est envoyé à l'application **"OCR Table"**. Si c'est une image ou un graphe, le contenu est envoyé à l'application **"OCR Figure"**. Ensuite, tous les résultats sont stockés dans une liste. 

La fonction "ocr_and_correction" prend en entrée le nom et le contenu du block de texte à extraire et retourne le résultat de l'extraction. Elle va tout d'abord envoyer l'entrée à l'application **"OCR Text"** et ensuite, le résultat sera envoyé à l'application **"Text Correction"**. C'est donc le resultat de la correction qui sera retourné. 

### Extract Real PDF

Les pages qui ne contiennent pas de graphes sont envoyées à la classe **"Extract Real PDF"** pour extraire le contenu de la page. 

La fonction "extract_text" prend entrée la page en cours de traitement, son nom ainsi que les blocks de tableau et d'image résultant de la segmentation. Elle retourne un JSON avec le nom de la page en clé et le résultat de l'extraction en valeur. Cette fonction va extraire tout d'abord les textes. Pour cela, on va envoyer le contenu de la page à la fonction "deduplicate_text" afin d'extraire le texte de la page et de garder seulement une fois les mots qui se sont dupliqués successivement. Elle retournera les textes dans une liste de string. La liste est envoyée à la fonction "supprimer_sauts_de_ligne" afin de garder la continuité des phrases sur la même ligne. Les blocks de tableau sont envoyés à l'application **"OCR Table"** et les blocks d'image sont envoyés à l'application **"OCR Figure"**. Ensuite, les résultats sont filtrés pour remonter les potentielles erreurs d'extraction en fonction des applications utilisées. Les résultats filtrés sont enfin stockés dans une liste puis retournés en JSON. 

### Send Request

Cette classe permet de gérer toutes les fonctions qui commnuniquent avec d'autres applications. Ici, on l'utilise pour communiquer avec les applications **"Convert PDF to Image"**, **"Segmentation Image to Blocks"**, **"OCR Text"**, **"OCR Figure"**, **"OCR Table"** et **"Text Correction"**.


![alt text](<Graph/Extract_real_pdf_graph.png>)