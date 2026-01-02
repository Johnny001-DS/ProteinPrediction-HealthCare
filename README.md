# CAFA 5 Protein Function Prediction with TensorFlow

This repository contains a solution for the [CAFA 5 Protein Function Prediction](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction) competition on Kaggle. The goal is to predict the function (Gene Ontology terms) of a set of proteins based on their amino acid sequences and other data.

## Overview

The project uses a Deep Neural Network (DNN) implemented in TensorFlow to predict Gene Ontology (GO) terms for proteins. Instead of processing raw protein sequences directly, the model utilizes pre-calculated protein embeddings generated using the Rost Lab's T5 protein language model.

## Dataset

The project relies on the following datasets:

1.  **CAFA 5 Competition Data**:
    - `train_sequences.fasta`: Protein sequences for the training set.
    - `train_terms.tsv`: Ground truth labels (protein ID, GO term ID, ontology aspect).
    - `test_sequences.fasta`: Protein sequences for the test set.
    - Available at: [Kaggle CAFA 5 Data](https://www.kaggle.com/competitions/cafa-5-protein-function-prediction/data)

2.  **T5 Protein Embeddings**:
    - Pre-calculated embeddings for the training and test sequences.
    - `train_embeds.npy`: Embeddings for training proteins.
    - `train_ids.npy`: Protein IDs corresponding to the training embeddings.
    - `test_embeds.npy`: Embeddings for test proteins.
    - `test_ids.npy`: Protein IDs corresponding to the test embeddings.
    - Created by Sergei Fironov, available at: [T5 Embeddings](https://www.kaggle.com/datasets/sergeifironov/t5embeds)

**Note**: To run the notebook, you need to download these datasets and place them in the appropriate directories as expected by the code (e.g., `/kaggle/input/`). You might need to adjust the file paths in the notebook if running locally.

## Prerequisites

To run the code, you need Python and the following libraries:

- tensorflow
- pandas
- numpy
- seaborn
- matplotlib
- progressbar2

You can install the dependencies using `pip`:

```bash
pip install -r requirements.txt
```

## Usage

1.  Clone this repository.
2.  Install the required dependencies.
3.  Download the datasets mentioned above.
4.  Open the Jupyter notebook `cafa-5-protein-function-with-tensorflow.ipynb`.
5.  Adjust the data paths in the notebook to match your local setup if necessary.
6.  Run the cells to train the model and generate predictions.

## Model Architecture

The model is a simple Deep Neural Network (DNN) with the following structure:

- **Input**: Protein embeddings (vector of length 1024).
- **Hidden Layers**: 3 Dense layers with 512 units each and ReLU activation. Batch Normalization is applied to the input.
- **Output Layer**: Dense layer with Sigmoid activation. The size depends on the number of target labels (top 1500 most frequent GO terms).
- **Loss Function**: Binary Crossentropy.
- **Optimizer**: Adam.

## Results & Submission

The notebook generates a `submission.tsv` file containing the predicted probabilities for each protein-GO term pair. This file follows the submission format required for the CAFA 5 competition.
