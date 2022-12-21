# Mega LM Pretraining

This repo contains a notebook used to pretrain a Mega architecture for masked language modeling (MLM). The goal of this effort was to produce a simple LM encoder which would be useful for the Hugging Face team to integrate Mega into the `transformers` library. I started with the `MegaEncoderLayer` class from the official Mega repo and added a vanilla PyTorch embedding layer and task prediction head for MLM.

Links:
* [Mega paper](https://arxiv.org/abs/2209.10655)
* [Mega repo](https://github.com/facebookresearch/mega)

## Training Details
I used `wikitext-103` as the text source, and I reused the BPE tokenizer used by RoBERTa and GPT2. I trained the model in Google Colab, which took a little over 5 hours on the free tier (using a T4 GPU). 

For the model architecture, I used a similar design as in the Mega paper for the LRA `Text` task (character-level text classification, see Appendix D in the Mega paper); most importantly, this consists of 4 encoder layers, rotary embeddings, no chunking, and hidden size of 128.

## Reuse
The model weights and tokenizer are stored in the Hugging Face model hub: https://huggingface.co/mnaylor/mega-wikitext-103

In order to load the pretrained weights, you'll need to install the Mega source code (see README in the Mega repo) and use the `MegaLM` and `MegaForMaskedLM` classes in the Colab notebook. Example code for instantiating the model class and loading the pretrained weights can be found at the bottom of the Colab notebook.
