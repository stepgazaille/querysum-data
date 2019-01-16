# Querysum dataset

Code for the dataset presented in the thesis *Query-Based Abstractive Summarization Using Neural Networks* by Johan Hasselqvist and Niklas Helmertz. The code for the model can be found at a [separate repo](https://github.com/helmertz/querysum).

## Requirements

- Python 3.5

Install required python packages using the following command:
```
pip install -r requirements.txt
```

Additionally, the NLTK data package `punkt` needs to be downloaded:
```
python -m nltk.downloader punkt
```


## Getting GloVe word embeddings
Use the following command to download and decompress the GloVe word embeddings:
```
wget "http://nlp.stanford.edu/data/glove.6B.zip"
mkdir glove
unzip glove.6B.zip -d glove
```

## Getting CNN/Daily Mail data
The dataset for query-based abstractive summarization is created by converting an existing dataset for question answering, released by [DeepMind](https://github.com/deepmind/rc-data). Archives containing the processed DeepMind dataset can be downloaded at [http://cs.nyu.edu/~kcho/DMQA/](http://cs.nyu.edu/~kcho/DMQA/), which we used. Both the `stories` and `questions` archives are required for the conversion, from either news organization, or both. To use both, merge the extracted directories, for `questions` and `stories` separately.


## Conversion
Replacing the parts in angle brackets, the dataset can be constructed by running:
```
python convert_rcdata.py \
    <path to stories directory> \
    <path to questions directory> \
    <path to output directory>
```
This creates separate directories in the output directory for training, validation and test sets.

For example:
```
python convert_rcdata.py ../DMQA/CNN/stories/ ../DMQA/CNN/questions/ ../DMQA/CNN/preproc/
python convert_rcdata.py ../DMQA/DM/stories/ ../DMQA/DM/questions/ ../DMQA/DM/preproc/
```

## Creating vocabularies
The repo contains a script for generating vocabularies, sorted by word frequency. They can be constructed by running:
```
python build_vocabularies.py \
    <path to dataset directory containing documents, queries and references> \
    <path to output directory, where document_vocabulary.txt, summary_vocabulary.txt and full_vocabulary.txt are saved>    
```

For example:
```
mkdir ../DMQA/CNN/vocabularies
python build_vocabularies.py ../DMQA/CNN/ ../DMQA/CNN/vocabularies
mkdir ../DMQA/DM/vocabularies
python build_vocabularies.py ../DMQA/DM/ ../DMQA/DM/vocabularies
```

