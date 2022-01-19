# Super Resolution GAN - Français

Présentation et implémentation d'un algorithme de deep learning appartenenant à la famille des GANs (Generative Adversarial Networks)

## Introduction GAN

Ce github est l'implémentation d'une variante du GAN qui se prénomme le SRGAN (Super Resolution GAN).  C'est un algorithme conçu pour un cas d'utilisation précis : la dépixélistaion d'images. On parle également de super résolution d'images. On note qu'il **existe** une multitude de variante au GAN tel que le StyleGAN ou le CycleGAN. Chaque algorithme est spécifique à un cas d'utilisation. 

> Ce projet est l'implémentation de l'algorithme du SRGAN décrit dans ce papier scientifique : [[1609.04802] Photo-Realistic Single Image Super-Resolution Using a Generative Adversarial Network (arxiv.org)](https://arxiv.org/abs/1609.04802)

## Objectif du PoC

L'objectif de l'algorithme est donc de faire de la super résolution d'images. L'algorithme reçoit en entrée une image de basse résolution et doit fournir en sortie une image de plus haute résolution. On parle de dépixélisation d'images. 

## Data

> Les données utilisées pour entrainer et tester l'algorithme proviennent du dataset div2k : [DIV2K Dataset (ethz.ch)](https://data.vision.ee.ethz.ch/cvl/DIV2K/)

Le dataset est composé de 800 images pour l'entrainement du modèle et 100 images de validation et de test.

## Fonctionnement de l'algorithme

## Exécution du projet

## Résultats obtenus

Voici les résultats obtenus : On a l'image initiale basse résolution que l'on fournit au générateur, l'image renvoyée par le générateur (l'image provenant de la super résolution) et l'image haute résolution correspondante pour comparer visuellement la performance de l'algorithme.

![Result1](https://github.com/Katalyse/Super-Resolution-GAN-Fr/blob/main/Image_Result/result_image_4.png)

![Result2](https://github.com/Katalyse/Super-Resolution-GAN-Fr/tree/main/Image_Result/result_image_56.png)

![Result3](https://github.com/Katalyse/Super-Resolution-GAN-Fr/tree/main/Image_Result/result_image_57.png)

![Result4](https://github.com/Katalyse/Super-Resolution-GAN-Fr/tree/main/Image_Result/result_image_63.png)
