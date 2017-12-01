# Gensim data

This repository keeps the models and datasets for the [gensim](https://github.com/RaRe-Technologies/gensim) download API. It serves as the data storage, and shouldn't be used directly (unless you're adding new datasets to it).

💡 When you use the gensim download API, **all data will be stored in the `~/gensim-data` folder**.

💡 Each dataset comes with its own original license, which the users should study before using the dataset. We are not the copyright holders, and are not responsible for any potential license breaches by users.

In current repository, all data stored as attachment files in [github-releases](https://github.com/RaRe-Technologies/gensim-data/releases)

## Quickstart

To load a model/dataset, use either the Python or command line interface:

- **Python API**

  Example: load a pre-trained model (gloVe word vectors)

  ```python
  import gensim.downloader as api

  info = api.info()  # show info about available models/datasets
  model = api.load("glove-twitter-25")  # download the model and return as object ready for use
  model.most_similar("cat")

  """
  output:

  [(u'dog', 0.9590819478034973),
   (u'monkey', 0.9203578233718872),
   (u'bear', 0.9143137335777283),
   (u'pet', 0.9108031392097473),
   (u'girl', 0.8880630135536194),
   (u'horse', 0.8872727155685425),
   (u'kitty', 0.8870542049407959),
   (u'puppy', 0.886769711971283),
   (u'hot', 0.8865255117416382),
   (u'lady', 0.8845518827438354)]

  """
  ```

  Example: load a corpus and use it to train Word2Vec

  ```python
  from gensim.models.word2vec import Word2Vec
  import gensim.downloader as api

  corpus = api.load('text8')  # download the corpus and return it opened as an iterable
  model = Word2Vec(corpus)  # train a model from the corpus
  model.most_similar("car")

  """
  output:

  [(u'driver', 0.8273754119873047),
   (u'motorcycle', 0.769528865814209),
   (u'cars', 0.7356342077255249),
   (u'truck', 0.7331641912460327),
   (u'taxi', 0.718338131904602),
   (u'vehicle', 0.7177008390426636),
   (u'racing', 0.6697118878364563),
   (u'automobile', 0.6657308340072632),
   (u'passenger', 0.6377975344657898),
   (u'glider', 0.6374964714050293)]

  """
  ```

  Example: **only** download and return the file path (no opening):

  ```python
  import gensim.downloader as api

  print(api.load("20-newsgroups", return_path=True))  # output: /home/user/gensim-data/20-newsgroups/20-newsgroups.gz
  print(api.load("glove-twitter-25", return_path=True))  # output: /home/user/gensim-data/glove-twitter-25/glove-twitter-25.gz
  ```

 - **CLI, command line interface**
   ```bash
   python -m gensim.downloader --info  # show info about available models/datasets
   python -m gensim.downloader --info text8  # download text8 dataset to ~/gensim-data/text8
   python -m gensim.downloader --download glove-twitter-25  # download model to ~/gensim-data/glove-twitter-50/
   ```

## Available data
### Datasets
| name | source | description |
|------|--------|-------------|
| 20-newsgroups | http://qwone.com/~jason/20Newsgroups/ | Collection of approximately 20,000 newsgroup documents, partitioned (nearly) evenly across 20 different newsgroups. |
| fake-news | https://www.kaggle.com/mrisdal/fake-news | News dataset, contains text and metadata from 244 websites and represents 12,999 posts in total from the past 30 days. The data was pulled using the webhose.io API, because it's coming from their crawler, not all websites identified by the BS Detector are present in this dataset. Data sources that were missing a label were simply assigned a label of 'bs'. There are (ostensibly) no genuine, reliable, or trustworthy news sources represented in this dataset (so far), so don't trust anything you read. |
| quora-duplicate-questions | https://data.quora.com/First-Quora-Dataset-Release-Question-Pairs | Over 400,000 lines of potential question duplicate pairs. Each line contains IDs for each question in the pair, the full text for each question, and a binary value that indicates whether the line truly contains a duplicate pair. |
| text8 | http://mattmahoney.net/dc/textdata | Cleaned small sample from Wikipedia. |
| wiki-english-20171001 | https://dumps.wikimedia.org/enwiki/20171001/ | Extracted Wikipedia dump from October 2017. Produced by `python -m gensim.scripts.segment_wiki -f enwiki-20171001-pages-articles.xml.bz2 -o wiki-en.gz` |

### Models
| name | description | papers | preprocessing | parameters |
|------|-------------|------------|--------|---------------|
| glove-twitter-100 | Pre-trained vectors based on  2B tweets, 27B tokens, 1.2M vocab, uncased (https://nlp.stanford.edu/projects/glove/) | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-twitter-100.txt`. | dimensions = 100 |
| glove-twitter-200 | Pre-trained vectors based on 2B tweets, 27B tokens, 1.2M vocab, uncased (https://nlp.stanford.edu/projects/glove/). | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-twitter-200.txt`. | dimensions = 200 |
| glove-twitter-25 | Pre-trained vectors based on 2B tweets, 27B tokens, 1.2M vocab, uncased (https://nlp.stanford.edu/projects/glove/). | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-twitter-25.txt`. | dimensions = 25 |
| glove-twitter-50 | Pre-trained vectors based on 2B tweets, 27B tokens, 1.2M vocab, uncased (https://nlp.stanford.edu/projects/glove/) | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-twitter-50.txt`. | dimensions = 50 |
| glove-wiki-gigaword-100 | Pre-trained vectors based on Wikipedia 2014 + Gigaword 5.6B tokens, 400K vocab, uncased (https://nlp.stanford.edu/projects/glove/). | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-wiki-gigaword-100.txt`. | dimensions = 100 |
| glove-wiki-gigaword-200 | Pre-trained vectors based on Wikipedia 2014 + Gigaword, 5.6B tokens, 400K vocab, uncased (https://nlp.stanford.edu/projects/glove/). | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-wiki-gigaword-200.txt`. | dimentions = 200 |
| glove-wiki-gigaword-300 | Pre-trained vectors based on Wikipedia 2014 + Gigaword, 5.6B tokens, 400K vocab, uncased (https://nlp.stanford.edu/projects/glove/). | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-wiki-gigaword-300.txt`. | dimensions = 300 |
| glove-wiki-gigaword-50 | Pre-trained vectors based on Wikipedia 2014 + Gigaword, 5.6B tokens, 400K vocab, uncased (https://nlp.stanford.edu/projects/glove/). | https://nlp.stanford.edu/pubs/glove.pdf | Converted to w2v format with `python -m gensim.scripts.glove2word2vec -i <fname> -o glove-wiki-gigaword-50.txt`. | dimension = 50 |
| word2vec-google-news-300 | Pre-trained vectors trained on part of Google News dataset (about 100 billion words). The model contains 300-dimensional vectors for 3 million words and phrases. The phrases were obtained using a simple data-driven approach described in 'Distributed Representations of Words and Phrases and their Compositionality' (https://code.google.com/archive/p/word2vec/). | https://arxiv.org/abs/1301.3781, https://arxiv.org/abs/1310.4546, https://www.microsoft.com/en-us/research/publication/linguistic-regularities-in-continuous-space-word-representations/?from=http%3A%2F%2Fresearch.microsoft.com%2Fpubs%2F189726%2Frvecs.pdf | - | dimension = 300 |


(generated by [generate_table.py](https://github.com/RaRe-Technologies/gensim-data/blob/master/generate_table.py) based on [list.json](https://github.com/RaRe-Technologies/gensim-data/blob/master/list.json))


# Want to add a new corpus or model?

1. Compress your data set using gzip or bz2.

2. Share the compressed file on any file-sharing service.

2. Create a [new issue](https://github.com/RaRe-Technologies/gensim-data/issues) and give us the dataset link. Add a **detailed description** on how you created the dataset, related papers or research, plus how users should use it. Include a code example where relevant.

----------------

`Gensim-data` is open source software released under the [LGPL license](https://github.com/rare-technologies/gensim-data/blob/master/LICENSE).

Copyright (c) 2017 [RaRe Technologies](https://rare-technologies.com/)
