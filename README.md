# pytorch-seq2seq

[![Build Status](https://travis-ci.org/IBM/pytorch-seq2seq.svg?branch=master)](https://travis-ci.org/IBM/pytorch-seq2seq)
[![Join the chat at https://gitter.im/pytorch-seq2seq/Lobby](https://badges.gitter.im/pytorch-seq2seq/Lobby.svg)](https://gitter.im/pytorch-seq2seq/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

**[Documentation](https://ibm.github.io/pytorch-seq2seq/public/index.html)**

**pytorch-seq2seq** is a simple, efficient and scalable framework implemented in [PyTorch](http://pytorch.org), to get you up and running in no time on sequence-to-sequence learning tasks.  The framework has modularized and extensible components for seq2seq models, training and inference, checkpoints, etc.  This is an alpha release. We appreciate any kind of feedback or contribution.


# What's New in 0.1.7

* Multi-GPU Support 
* Copy Attention mechanism
* Fully compatible with the latest PyTorch 0.4.1

# Roadmap
Sequence to sequence learning is a fast evolving space with new techniques and architectures being published frequently.  The goal of this library is facilitating the development of such techniques and applications.  While constantly improving the quality of code and documentation, we will focus on the following items:

* Tutorials with examples on how to quickly get started with the library;
* Evaluation with benchmarks such as WMT machine translation, COCO image captioning, conversational models, etc;
* Provide more flexible model options and improve the usability of the library;
* Adding latest architectures such as the CNN based model proposed by [Convolutional Sequence to Sequence Learning](https://arxiv.org/abs/1705.03122), the transformer model proposed by [Attention Is All You Need](https://arxiv.org/abs/1706.03762) and the deep reinforced model proposed by [A Deep Reinforced Model for Abstractive Summarization](https://arxiv.org/abs/1705.04304);
* Support features in the new versions of PyTorch.

# Installation
This package requires Python 2.7 or 3.6. We recommend creating a new virtual environment for this project (using virtualenv or conda).  

### Prerequisites

* Numpy: `pip install numpy` (Refer [here](https://github.com/numpy/numpy) for problem installing Numpy).
* PyTorch: Refer to [PyTorch website](http://pytorch.org/) to install the version w.r.t. your environment.

### Install from source
Currently we only support installation from source code using setuptools.  Checkout the source code and run the following commands:

    pip install -r requirements.txt
    python setup.py install

If you already had a version of PyTorch installed on your system, please verify that it is at least `v0.4.1` for compatibility with our latest release `v0.1.7`.

# Get Started
### Prepare toy dataset

	# Run script to generate the reverse toy dataset
    # The generated data is stored in data/toy_reverse by default
	scripts/toy.sh

### Train and play
	TRAIN_PATH=data/toy_reverse/train/data.txt
	DEV_PATH=data/toy_reverse/dev/data.txt
	# Start training
    python examples/sample.py --train_path $TRAIN_PATH --dev_path $DEV_PATH

It will take about 3 minutes to train on CPU and less than 1 minute with a Tesla K80.  Once training is complete, you will be prompted to enter a new sequence to translate and the model will print out its prediction (use ctrl-C to terminate).  Try the example below!

    Input:  1 3 5 7 9
	Expected output: 9 7 5 3 1 EOS

### Checkpoints
Checkpoints are organized by experiments and timestamps as shown in the following file structure

    experiment_dir
	+-- input_vocab
	+-- output_vocab
	+-- checkpoints
	|  +-- YYYY_mm_dd_HH_MM_SS
	   |  +-- decoder
	   |  +-- encoder
	   |  +-- model_checkpoint

The sample script by default saves checkpoints in the `experiment` folder of the root directory.  Look at the usages of the sample code for more options, including resuming and loading from checkpoints.

# Benchmarks

* WMT Machine Translation (Coming soon)

# Troubleshoots and Contributing
If you have any questions, bug reports, and feature requests, please [open an issue](https://github.com/IBM/pytorch-seq2seq/issues/new) and make sure to use labels, to make everyone's life easier.  For live discussions, please go to our [Gitter lobby](https://gitter.im/pytorch-seq2seq/Lobby).

We appreciate any kind of feedback or contribution.  Feel free to proceed with small issues like questions, bug fixes and documentation improvement.  For major contributions and new features, please discuss with the collaborators in corresponding issues.  

### Development Cycle
We are using 4-week release cycles, where during each cycle changes will be pushed to the `develop` branch and finally merge to the `master` branch at the end of each cycle.

### Development Environment
We setup the development environment using [Vagrant](https://www.vagrantup.com/).  To get started, make sure that you have [VirtualBox](https://www.virtualbox.org/) installed on your system, then run `vagrant up` with our 'Vagrantfile', once the VM has been provisioned you can `vagrant ssh` into it and start moving things around, albeit in moderation.

The following tools are needed and installed in the development environment by default:
* Git
* Python 2.7
* Python packages: pytorch, torchtext, nose, mock, coverage, flake8

[Docker](https://www.docker.com/) support for development coming soon.

### Test
The quality and the maintainability of the project is ensured by comprehensive tests.  We encourage writing unit tests and integration tests when contributing new codes.

Locally please run `nosetests` in the package root directory to run unit tests.  We use TravisCI to require that a pull request has to pass all unit tests to be eligible to merge.  See [travis configuration](https://github.com/IBM/pytorch-seq2seq/blob/master/.travis.yml) for more information.

### Code Style
We follow [PEP8](https://www.python.org/dev/peps/pep-0008/) for code style.  Especially the style of docstrings is important to generate documentation.

* *Local*: Run the following commands in the package root directory
```
# Python syntax errors or undefined names
flake8 . --count --select=E901,E999,F821,F822,F823 --show-source --statistics
# Style checks
flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
```
* *Github*: We use [Codacy](https://www.codacy.com) to check styles on pull requests and branches.
