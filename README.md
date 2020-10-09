# Adapter-BERT
## Introduction

This is an implementation of [Parameter-Efficient Transfer Learning for NLP](http://proceedings.mlr.press/v97/houlsby19a.html).

## Extensions
We propose and implement two extensions to Houlsby’s architecture to investigate the
impact of parameter sharing of adapters across BERT model.

### First extension
As a first extension to Houlsby’s architecture (further referred to as not shared), we make three
changes in the model. First, we unfreeze norms layer of encoders in BERT model and allow them to
fine-tune during training adapters. Second, two adapters in each layer are not shared. Finally, we add
two classifier layers on the top of the pooler with Tanh activation function between them. To do so,
the total number of parameters added per layer, including biases, is 4md + 2d + 2m

### Second extension

As a second extension (further referred to as 3-shared), we follow Houlsby’s architecture, but instead
of sharing adapters in each layer, we share them in all three consecutive layers. The intuition
comes from that several studies have proven that different layers of BERT encode
different types of knowledge like surface, syntactic, and semantic information Jawahar et al. (2019).
Additionally, due to multiplying outputs with input embedding weights in MLM objective of BERT
during pre-training to restore high representations to the vocabulary representation, the last three
layers of BERT play nearly a same role in the model.

### Results
According to our extensions' results, we significantly reduced the number of model's parameters while the performance is not hurt substantially.
More details can be found in the Report.pdf
