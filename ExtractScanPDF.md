# Extract Scan PDF

## Entrée : Nom et corps du fichier PDF + liste des numéros de page

## Sortie : Liste de String

Cette application traite l'extraction du contenu des pages du fichier PDF considérées comme "PDF scannés ".

## Controller

Le nom et le corps du fichier PDF sont envoyés à la classe **"Controller"** ainsi que la liste des numéros des pages détéctées comme "PDF scannés". Le PDF sera divisé en block de 10 pages à traiter en même temps. Il est ensuite convertie en base 64 pour être envoyé à fonction "all_ocr_process".

La fonction "all_ocr_process" prend en entrée le nom du PDF, le PDF en base 64 et la liste des numéros de pages et retourne la liste des résultats de l'extraction du contenu de fichier.  Elle va tout d'abord envoyer ces éléments à l'application **"Convert PDF to Image"**. Les images seront ensuite envoyées à la fonction "segementation_ocr_correction_image_to_text". 

La fonction "segementation_ocr_correction_image_to_text" prend entrée les images et retourne la liste des résultats de l'extraction du fichier. Les images sont envoyées à la fonction "process_image". Le résultat est ensuite remis dans une liste par block de 10 images. 

La fonction "process_image" prend en entrée le nom de l'image et l'image elle-même. Elle est ensuite envoyée à l'application **"Segmentation Image to Blocks"**. Le résultat est stocké dans des variables séprarée pour tous les blocks de texte, tableau, image et graphe. Si c'est un texte, le contenu est envoyé à la fonction "ocr_and_correction". Si c'est un tableau, le contenu est envoyé à l'application **"OCR Table"**. Si c'est une image ou un graphe, le contenu est envoyé à l'application **"OCR Figure"**. Ensuite, tous les résultats sont stockés dans une liste. 

La fonction "ocr_and_correction" prend en entrée le nom et le contenu du block de texte à extraire et retourne le résultat de l'extraction. Elle va tout d'abord envoyer l'entrée à l'application **"OCR Text"** et ensuite, le résultat sera envoyé à l'application **"Text Correction"**. C'est donc le resultat de la correction qui sera retourné. 

### Send Request

Cette classe permet de gérer toutes les fonctions qui commnuniquent avec d'autres applications. Ici, on l'utilise pour communiquer avec les applications **"Convert PDF to Image"**, **"Segmentation Image to Blocks"**, **"OCR Text"**, **"OCR Figure"**, **"OCR Table"** et **"Text Correction"**.

