# Paraphrasing SCPN 
## 1. Goal of the project
Code to train models from "Adversarial Example Generation with Syntactically Controlled Paraphrase Networks".

Paraphrasing a given sentence into 10 sentences with different grammatical structures.

## 2. Requirement for library installation
The code is written in python and requires PyTorch 3.1.
```
pip install torch
```

## 3. Guide for train and test
### Getting started
Download trained models (scpn.pt and parse_generator.pt) from https://drive.google.com/file/d/1AuH1aHrE9maYttuSJz_9eltYOAad8Mfj/view?usp=sharing and place them in the models directory.

This code is run on GPU, if you don't have GPU, please change torch.load function with map_location=torch.device('cpu')

### Training
Download the training data from https://drive.google.com/file/d/1x1Xz3KQP_Ncu3DVPhOCsAwwOlFgcre5H/view?usp=sharing and move it to the data folder. 

Train a model from scratch with default settings run train.sh.

    sh train.sh
or
    
    python train_scpn.py

Check train_scpn.py for training command line options. Some of important options:

    --data: hdf5 location, default='data/parsed_data.h5
    --model: model save path, default='scpn2.pt'
    --n_epochs: number of epochs n_epochs, default=15
    --save_freq: how many minibatches to save model, default=50
    --init_trained_model: continue training a cached model, default=0
    
Train with a cached model and save model after every 200 minibaches:

    python train_scpn.py --data=yourdatapath --init_trained_model=1 --save_freq=200
    
### Testing
There is also a demo script (run demo.sh) that will generate paraphrases from a set of templates 

    sh demo.sh
    
Check the script to see available choices. The input file is written as a csv file with 3 attributes idx, tokens, parse:
    
    --out_file: paraphrase save path, default='scpn_ex.out'
    --parsed_input_file: parse load path, default='data/scpn_ex.tsv'
    --pp_model: paraphrase model to load, default='models/scpn.pt'
    --parse_model: model save path, default='models/parse_generator.pt'

Example:

    python generate_paraphrases.py --parsed_input_file input.tsv --out_file output.txt

## 4. Reference (Paper, Github link)
You can visit the links below for more detail:

Github: https://github.com/miyyer/scpn

Paper: https://arxiv.org/pdf/1804.06059.pdf
