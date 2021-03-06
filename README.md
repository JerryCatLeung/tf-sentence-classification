# Sentence Classification in TensorFlow

This project is roughly an exact TensorFlow implementation of Yoon Kim's paper [Convolutional Neural Networks for Sentence Classification](https://arxiv.org/abs/1408.5882) (EMNLP 2014). His original Theano code can be found [here](https://github.com/yoonkim/CNN_sentence). Alternate to this, you can look at Denny Britz's TensorFlow implementation, [here](https://github.com/dennybritz/cnn-text-classification-tf).

## Setup

1. Download Google's `word2vec` embeddings and place them inside `data/w2v/`. This is a large file (~ `3.5G`). You may `git clone` [this](https://github.com/mmihaltz/word2vec-GoogleNews-vectors).
2. Ensure you have a working `tensorflow` or `tensorflow-gpu` (version 1.0+). Additional dependencies include `yaml`, `bunch` and `cPickle`.
3. Pre-process the data by using,
```
cd data
chmod +x process_sst2.sh process_sst2_sentence.sh
./process_sst2.sh
./process_sst2_sentence.sh
```
4. Run `python train.py` to train the model, and run `python train.py --mode test` to evaluate the model.

## Model Configuration
The model hyperparameters and mode (`nonstatic`, `static` and `rand`) are configured via YAML files inside `config/`. All hyperparameters (except `batch_size`) are identical to those reported in the paper. You may change the training directory via the `--job_id` parameter, and the random seed using `--seed`. Look at `config/arguments.py` for more details.

## Results
All results have been averaged across 10 random seeds. All reported results are on the [SST2 dataset](https://nlp.stanford.edu/sentiment/treebank.html). The models were trained on Titan X GPUs.

Model | Dataset | Average | Std | Range |
| ------------- |:-------------:|:-----:|:-----:|:-----:|
[Kim14](https://arxiv.org/abs/1408.5882) - nonstatic | Phrases | 87.2 | - | - |
Our [Kim14](https://arxiv.org/abs/1408.5882) - nonstatic | Phrases | 87.06 | 0.34 | 86.55 - 87.70 |
Our [Kim14](https://arxiv.org/abs/1408.5882) - nonstatic | Sentences | 85.92 | 0.68 | 84.79 - 86.99 |
[Kim14](https://arxiv.org/abs/1408.5882) - rand | Phrases | 82.7 | - | - |
Our [Kim14](https://arxiv.org/abs/1408.5882) - rand | Phrases | 84.53 | 0.38 | 84.01 - 85.01 |
Our [Kim14](https://arxiv.org/abs/1408.5882) - rand | Sentences | 79.65 | 0.89 | 77.76 - 81.00 |
[Kim14](https://arxiv.org/abs/1408.5882) - static | Phrases | 86.8 | - | - |
Our [Kim14](https://arxiv.org/abs/1408.5882) - static | Phrases | 86.10 | 0.58 | 85.23 - 86.82 |
Our [Kim14](https://arxiv.org/abs/1408.5882) - static | Sentences | 85.18 | 0.66 | 83.69 - 86.32 |

## Contributing
Feel free to add Issues and PRs (for the existing issues). It should be fairly easy to understand the code.
