# Super Resolution GAN - Français

Présentation et implémentation d'un algorithme de deep learning appartenenant à la famille des GANs (Generative Adversarial Networks)

## Introduction GAN

Ce github est l'implémentation d'une variante du GAN qui se prénomme le SRGAN (Super Resolution GAN).  C'est un algorithme conçu pour un cas d'utilisation précis : la dépixélistaion d'images. On parle également de super résolution d'images. On note qu'il **existe** une multitude de variante au GAN tel que le StyleGAN ou le CycleGAN. Chaque algorithme est spécifique à un cas d'utilisation. 

> Ce projet est l'implémentation de l'algorithme du SRGAN décrit dans ce papier scientifique : [[1609.04802] Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network (arxiv.org)](https://arxiv.org/abs/1609.04802)

## Objectif du PoC

L'objectif de l'algorithme est donc de faire de la super résolution d'images. L'algorithme reçoit en entrée une image de basse résolution et doit fournir en sortie une image de plus haute résolution.

## Data

> Les données utilisées pour entrainer et tester l'algorithme proviennent du dataset div2k : [DIV2K Dataset (ethz.ch)](https://data.vision.ee.ethz.ch/cvl/DIV2K/)

Le dataset est composé de 800 images pour l'entrainement du modèle et 100 images de validation et de test.

## Fonctionnement de l'algorithme

Pour mieux comprendre le fonctionnement d'un GAN ou d'un SRGAN, je vous invite à lire cet article :

Au niveau de l'implémentation, on a :

* la fonction load_dataset() récupère le nom de tous les fichiers du dossier donné en paramètre (il faut que ce dossier ne contient que les images que l'on souhaite utiliser dans l'algorithme). La fonction vient en suite charger les images, les resize selon le shape que l'on souhaite puis les transforme en numpy array. On renvoie une liste des images sous la forme numpy array
* la fonction normalisation prend en entrée la liste des images et applique une normalisation pour que les pixels soient compris entre [-1,1] au lieu de [0,255]. Cela facilite l'apprentissage de l'algorithme
* la fonction prediction_et_resultat_plot prend en entrée les deux bases de test et le generateur. On tire aléatoirement un certain nombre d'images dans les deux bases de test. Si on est en mode "entrainement", on prédit les images à l'aide du générateur. Si l'on est en mode "prediction", on charge les poids du generateur pour obtenir le generateur entrainé puis on prédit. On dénormalise les images puis on peut afficher les trois images côte à côte (l'image basse résolution, l'image générée et l'image haute résolution).
* la fonction creation_vgg() charge le réseau VGG déjà entrainé (une fonction existe sous Keras)
* les fonctions creation_discriminateur() et creation_generateur() sont les réseaux de neurones décrit ci-desssous en provenant du papier de recherche officiel du SRGAN.
![Result1](https://github.com/Katalyse/Super-Resolution-GAN-Fr/blob/main/Image_Readme/SRGAN_architecture.png)
* la fonction creation_SRGAN() regroupe les trois modèles distincts pour former le SRGAN
* la fonction train() est la fonction d'entrainement. on fait une boucle suivant le nombre d'epochs. Pour chaque itération, on tire un certain nombre d'images dans la base d'entrainement. On prédit les images basses résolutions puis on entraine le discriminateur avec les images réelles et générées. On tire un nouveau jeu d'images dans la base d'entrainement puison entraine notre SRGAN pour entrainer notre générateur. On affiche les résultats au cours de l'exécution et on sauvegarde les poids des modèles.
* Enfin, on a le main qui appelle l'ensemble des fonctions.

## Requierements

Le fichier requirements.txt liste les librairies et les versions correspondantes utilisées pour exécuter le script. L'exécution du script en mode entrainment avec une NVIDIA Tesla M60 (dans le cloud Azure) prend une vingtaine d'heure.

## Exécution du projet

Pour télécharger les données, vous pouvez utiliser le fichier download_data.ipynb. Ce sont simplement des commandes pour télécharger puis dézipper les quatre datasets (images d'entrainement basse résolution / haute résolution / images de test basse résolution / haute résolution.

Une fois que les données sont à disposition on peut lancer le notebook SRGAN.ipynb. On a une fonction pour charger les données, une autre pour les normaliser. On a ensuite une fonction de scoring et d'affichage des données. On a trois fonctions pour créer les trois réseaux de neurones dont nous aurons besoin (le discriminateur, le générateur, le VGG) puis une fonction finale pour joindre les trois modèles et former le SRGAN. Enfin, on a la fonction d'entrainement de l'algorithme puis le main pour charger, normaliser puis soit entrainer le modèle soit utiliser le modèle déjà entrainé. En effet, vous pouvez aussi tester l'algorithme sans entrainement puisque les poids du générateur sont enregistrés dans le fichier au format .h5 disponible dans ce github. Il suffit de alors de créer le modèle et de charger ses poids pour éviter la phase d'entrainement de l'algorithme.

## Résultats obtenus

Voici les résultats obtenus : On a l'image initiale basse résolution que l'on fournit au générateur, l'image renvoyée par le générateur (l'image provenant de la super résolution) et l'image haute résolution correspondante pour comparer visuellement la performance de l'algorithme.

![Result1](https://github.com/Katalyse/Super-Resolution-GAN-Fr/blob/main/Image_Result/result_image_4.png)

![Result2](https://github.com/Katalyse/Super-Resolution-GAN-Fr/blob/main/Image_Result/result_image_56.png)

![Result3](https://github.com/Katalyse/Super-Resolution-GAN-Fr/blob/main/Image_Result/result_image_57.png)

![Result4](https://github.com/Katalyse/Super-Resolution-GAN-Fr/blob/main/Image_Result/result_image_63.png)
