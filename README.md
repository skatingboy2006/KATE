KATE: K-Competitive Autoencoder for Text
===============

Code & data accompanying the KDD2017 paper ["KATE: K-Competitive Autoencoder for Text"](https://arxiv.org/abs/1705.02033)

## Prerequisites
This code is written in python. To use it you will need:
- Python 2.7
- A recent version of [Numpy](http://www.numpy.org)
- A recent version of [NLTK](http://www.nltk.org)
- [Tensorflow = 1.15.2](https://www.tensorflow.org)
- [Keras = 2.0.6](https://keras.io)

## Getting started

To preprocess the corpus, e.g., 20 Newsgroups, just run the following:

```bash
    python construct_20news.py -train [train_dir] -test [test_dir] -o [out_dir] -threshold [word_freq_threshold] -topn [top_n_words]
```
It outputs 4 json files under the [out_dir] directory: train\_data, train\_label, test\_data and test\_label.
You can <b>download the preprocessed data</b> we used in our experiments [here](http://academic.hugochan.net/download/KATE-preprocessed-data.zip).



To train the KATE model, just run the following:

```bash
    python train.py -i [train_data] -nd [num_topics] -ne [num_epochs] -bs [batch_size] -nv [num_validation] -ctype kcomp -ck [top_k] -sm [model_file]
```

To predict on the test set, just run the following:

```bash
    python pred.py -i [test_data] -lm [model_file] -o [output_doc_vec_file] -st [output_topics] -sw [output_sample_words] -wc [output_word_clouds]
```


To train a simple classifier, just run the following:

```bash
  python run_classifier.py [train_doc_codes] [train_doc_labels] [test_doc_codes] [test_doc_labels] -nv [num_validation] -ne [num_epochs] -bs [batch_size]
```

To train baseline methods, e.g., VAE, just run the following:

```bash
     python train_vae.py -i [train_data] -nd [num of dimensions] -ne [num_epochs] -bs [batch_size] -nv [num_validation] -sm [model_file]
```



## Notes

1) In order to apply the KATE model to your own dataset, you will need to preprocess the dataset on your own. Basically, prepare the vocabulary and Bag-of-Words representation of each document.

2) The KATE model learns vector representations of words (which are in the vocabulary) as well as documents in an unsupervised manner. It can also extracts topics from corpus. Document labels will be needed only if you want to for example train a document classifier based on learned document vectors.

## FAQ


1) KeyError when plotting word clouds

  Make sure the words belong to the vocabulary. See [here](https://github.com/hugochan/KATE/issues/9).



## Architecture

<center><img src="img/kate_arch.png" width="600" height="400" /></center>


## Experiment results on 20 Newsgroups

### PCA on the 20-D document vectors
![20news_doc_vec_pca](img/20news_doc_vec_pca.png "20news_doc_vec_pca")

### TSNE on the 20-D document vectors
![20news_doc_vec_tsne](img/20news_doc_vec_tsne.png "20news_doc_vec_tsne")

### Five nearest neighbors in the word representation space
![20news_word_vec](img/20news_word_vec.png "20news_word_vec")

### Extracted topics

<center><img src="img/20news_topics.png" width="600" height="500" /></center>

### Text classification results on 20 Newsgroups

<center><img src="img/20news_doc_clf.png" width="300" height="400" /></center>


### Visualization of the normalized topic-word weight matrices of KATE & LDA (KATE learns distinctive patterns)

<center><img src="img/vis_pattern.png" width="900" height="350" /></center>


## Reference

If you found this code useful, please cite the following paper:

Yu Chen and Mohammed J. Zaki. **"KATE: K-Competitive Autoencoder for Text."** *In Proceedings of the ACM SIGKDD International Conference on Data Mining and Knowledge Discovery. Aug 2017.*

    @inproceedings {chen2017kate,
    author = { Yu Chen and Mohammed J. Zaki },
    title = { KATE: K-Competitive Autoencoder for Text },
    booktitle = { Proceedings of the ACM SIGKDD International Conference on Data Mining and Knowledge Discovery },
    doi = { http://dx.doi.org/10.1145/3097983.3098017 },
    year = { 2017 },
    month = { Aug }
    }

Other research papers that applied the KATE model:

Chen, Yu, Rhaad M. Rabbani, Aparna Gupta, and Mohammed J. Zaki. "Comparative text analytics via topic modeling in banking." In 2017 IEEE Symposium Series on Computational Intelligence (SSCI), pp. 1-8. IEEE, 2017.

	@inproceedings{chen2017comparative,
	  title={Comparative text analytics via topic modeling in banking},
	  author={Chen, Yu and Rabbani, Rhaad M and Gupta, Aparna and Zaki, Mohammed J},
	  booktitle={2017 IEEE Symposium Series on Computational Intelligence (SSCI)},
	  pages={1--8},
	  year={2017},
	  organization={IEEE}
	}
