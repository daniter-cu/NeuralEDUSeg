# Neural-EDU-Segmentation
A toolkit for segmenting Elementary Discourse Units (clauses).
We implement it as is described in our EMNLP paper: [Toward Fast and Accurate Neural Discourse Segmentation](http://www.aclweb.org/anthology/D18-1116)


### Requirements
- Python 3.5
- Tensorflow>=1.5.0
- allennlp>=0.4.2
- See `requirements.txt` for the full list of packages

### Data

We cannot provide the complete [RST-DT corpus](https://catalog.ldc.upenn.edu/products/LDC2002T07) due to the LDC copyright.
So we only put several samples in `./data/rst/` to test the our code and show the data structure.

If you want to train or evaluate our model on RST-DT, you need to download the data manually and put it in the same folder. Then run the following command to preprocess the data and create the vocabulary:

```
python run.py --prepare
```


### Evaluate the model on RST-DT:

We provide the vocabulary and a well-trained model in the `./data/` folder. You can evaluate the performance of this model after preparing the RST-DT data as mentioned above:

```
python run.py --evaluate --test_files ../data/rst/preprocessed/test/*.preprocessed
```

The performance of current model should be as follows:
```
'precision': 0.9176470588235294, 'recall': 0.975, 'f1': 0.9454545454545454}
```

Note that this is slightly better than the results we reported in the paper, since we re-trained the model and there is some randomness here.

### Train a new model

You can use the following command to train the model from scratch:

```
python run.py --train
```

Hyper-parameters and other training settings can be modified in `config.py`.

### Segmenting raw text into EDUs

You can segment files with raw text into EDUs:

```
python run.py --segment --input_files ../data/rst/TRAINING/wsj_110*.out --result_dir ../data/results/
```

The segmented result for each file will be saved to the `--result_dir` folder with the same name. Each EDU is written as a line.


### Citation

Please cite the following paper if you use this toolkit in your work:

```
@inproceedings{wang2018edu,
  title={Toward Fast and Accurate Neural Discourse Segmentation},
  author={Wang, Yizhong and Li, Sujian and Yang, Jingfeng},
  booktitle={Proceedings of the 2018 Conference on Empirical Methods in Natural Language Processing},
  pages={962--967},
  year={2018}
}
```


# DANITER Notes:

This code is a bit dated so here are the steps to get this running on Sept 2021

EDU segmenter details:  
* use python 3.6  
* install allennlp from source - https://github.com/allenai/allennlp/releases/tag/v0.4.2  
--  
pip install -U pip setuptools wheel  
pip install --editable .  
pip install -r requirements.txt  
allennlp test-install  
-- 

* fix allen bug pip install overrides==3.1.0  
* replace from scipy.optimize import linear_sum_assignment as linear_assignment 
In <PATH>/eduseg/allennlp-0.4.2/allennlp/training/metrics/conll_coref_scores.py  


Run eduseg in allennlp conda env.
Install old version of tensorflow	(pip install tensorflow==1.5.0)

Must run on GPU machine...