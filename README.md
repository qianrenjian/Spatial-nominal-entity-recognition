# Spatial Nominal Entity Recognition


## Overview

This repository contains the source code for evaluating ML models trained for Spatial Nominal Entity Recognition as proposed in 

> Amine Medad, Mauro Gaio Ludovic Moncla, Sébastien Mustière, and Yannick Le Nir. Comparing supervised learning algorithms for Spatial Nominal Entity recognition. The 23rd AGILE International Conference on Geographic Information Science. 2020


Datasets are given in the `corpus` directory and models in the `models` directory. 
You need first to download the binary file of the pretrained French [FastText model](https://dl.fbaipublicfiles.com/fasttext/vectors-crawl/cc.fr.300.bin.gz) and add it to the model directory.

## Run the code

	python3 evaluate_model_snoer.py -i <input_dataset> -n <ngram_size> -alg <algorithm_name> -m <model_filepath> -ft <fasttext_model> -fr_nouns <french_nouns_filepath> -s <we_size_vec> -ti <train_dataset>

 * `<input_dataset>`: filepath to the csv input data
 * `<train_dataset>`: filepath to the csv training data (use for PCA fitting for the model MLP+PCA only)
 * `<fasttext_model>`: filepath of the pretrained FastText binary model
 * `<french_nouns_filepath>`: filepath of the file containing French nouns (use for padding ngrams)
 * `<algorithm_name>`: name of the architecture used for training (GRU, MLP+AE, MLP+PCA, SVM, RF)
 * `<model_filepath>`: filepath of the model to evaluate
 * `<ngram_size>`: size of the ngram (1, 5 or 7)
 * `<we_size_vec>`: Word Embedding dimension (default: 300)

 You can also download and execute the jupyter notebook version.

## Example

Run the following command to evaluate the GRU model trained with 5 grams :

    python3 evaluate_model_snoer.py -i "./data/corpus_validation.csv" -n 5 -alg "GRU" -m "./models/GRU_5grams.h5" -ft "./data/cc.fr.300.bin" -fr_nouns "./data/French_nouns.txt" -ti "./data/corpus_train.csv" 
    

## Results

| Model 	<td colspan=3>GRU</td> <td colspan=3>RF</td> <td colspan=3>SVM</td>
|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|-	|
| ngram_size 	| 1 g 	| 5 g 	| 7 g 	| 1 g 	| 5 g 	| 7 g 	| 1 g 	| 5 g 	| 7 g 	|
| Accuracy 	| 0.67 	| 0.76 	| 0.79 	| 0.76 	| 0.73 	| 0.74 	| 0.69 	| 0.75 	| 0.72 	|

| Model 	<td colspan=3>MLP + AE</td> <td colspan=3>MLP + PCA</td> 
|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|:-:	|
| ngram_size 	| 1 g 	| 5 g 	| 7 g 	| 1 g 	| 5 g 	| 7 g 	|
| Accuracy 	| 0.68 	| 0.75 	| 0.78 	| 0.49 	| 0.64 	| 0.60 	|



## Acknowledgement

This work is supported and financed by French National Research Agency (ANR) under the CHOUCAS project (ANR-16-CE23-0018). 

The [CHOUCAS project](http://choucas.ign.fr) is a French interdisciplinary research project aiming to respond to a need expressed by the high mountain gendarmerie platoon to help localising victims in mountain area.
