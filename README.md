# Codes-for-Lifelong-Learning-of-Topics-and-Domain-Specific-Word-Embeddings
Codes for "Lifelong Learning of Topics and Domain-Specific Word Embeddings"

First, run dataprocess.py to finish dataprocessing. Then, run build_svm_dataset.py to generate processed dataset for word embedding downstream tasks. Finally, run python cllm_amazon_parameter_npmi.py -d data_correct\Ama for LCM.
	
Due to the limited space of the paper, we provide the search space of hyperparameters for grid search in all of our baselines and their corresponding best hyperparameters.

### LDA-LTM

| parameter   | search scale |
| ----------- | ------------ |
| nBurnin     | [200, 500]   |
| nIterations | [1000, 2000] |
| sampleLag   | [10, 20]     |
| alpha       | [0.1, 1.0]   |
| beta        | [0.01, 0.1]  |

best parameters:

| metrics | nBurnin | nIterations | sampleLag | alpha | beta |
| ------- | ------- | ----------- | --------- | ----- | ---- |
| npmi    | 200     | 1000        | 10        | 0.1   | 0.1  |
| TU      | 200     | 1000        | 20        | 0.1   | 0.1  |
| perp    | 200     | 2000        | 10        | 1.0   | 0.1  |



### LNTM

| parameter  | search scale  |
| ---------- | ------------- |
| iter_num   | [200, 400]    |
| lambda_emb | [0.1, 1.0]    |
| sal_gamma  | [0.1, 1.0]    |
| sal_thresh | [1.0, 10.0]   |
| ll_lambda  | [0.001, 0.01] |

best parameters:

| metrics | iter_num | lambda_emb | sal_gamma | sal_thresh | ll_lambda |
| ------- | -------- | ---------- | --------- | ---------- | --------- |
| npmi    | 400      | 0.1        | 0.1       | 1.0        | 0.001     |
| TU      | 400      | 1.0        | 0.1       | 1.0        | 0.01      |
| perp    | 400      | 0.1        | 0.1       | 1.0        | 0.001     |



### NMF-LTM

| parameter  |    search scale   |
| ---------- | ----------------- |
| iter_num   | [50, 100, 200]    |
| alpha      | [0.1, 1.0, 10]    |
| beta       | [0.1, 0.5, 1.0]   |
| eta        | [0.001, 0.01, 0.1]|

best parameters:

| metrics | iter_num | alpha | beta | eta  |
| ------- | -------- | ----- | -----| -----|
| npmi    | 200      | 10    | 0.5  | 0.001|
| TU      | 200      | 10    | 1.0  | 0.001|
| perp    | 200      | 10    | 0.1  | 0.001|



### Word2Vec/FastText

| parameter       | search scale    |
| --------------- | --------------- |
| learning_rate   | [0.025, 0.05]   |
| win_size        | [5, 7]          |
| negative_thresh | [0.0001, 0.001] |
| negative_size   | [5, 10]         |
| lr_update       | [100, 200]      |

best parameters:

| metrics | learning_rate | win_size | negative_thresh | negative_size | lr_update |
| ------- | ------------- | -------- | --------------- | ------------- | --------- |
| svm     | 0.05          | 7        | 0.001           | 10            | 100       |



### L-DEM

| parameter     | search scale             |
| ------------- | ------------------------ |
| win_size      | [3, 5, 7]                |
| epochs        | [1, 3]                   |
| learning_rate | [0.00001, 0.0001, 0.001] |
| negative_size | [5, 10]                  |

best parameters:

| metrics | win_size | epochs | learning_rate | negative_size |
| ------- | -------- | ------ | ------------- | ------------- |
| svm     | 7        | 3      | 0.00001       | 5             |



### SPINE

| parameter | search scale       |
| --------- | ------------------ |
| epochs    | [1000, 2000, 4000] |
| noise     | [0.2, 0.4]         |
| sparsity  | [0.5, 0.75, 0.85]  |

best parameters:

| metrics | epochs | noise | sparsity |
| ------- | ------ | ----- | -------- |
| svm     | 1000   | 0.4   | 0.85     |



### Word2Sense

| parameter     | search scale  |
| ------------- | ------------- |
| topic_num     | [500, 1000]   |
| iterations    | [300, 500]    |
| alpha         | [0.01, 0.1]   |
| beta          | [0.001, 0.01] |
| embedding_nnz | [10, 20]      |

best parameters:

| metrics | topic_num | iterations | alpha | beta | embedding_nnz |
| ------- | --------- | ---------- | ----- | ---- | ------------- |
| svm     | 1000      | 300        | 0.1   | 0.01 | 20            |

Notes:
In Section 4.5.4, we propose that "For all domains, the latest KG will not have a significant negative impact on LCM (i.e., the catastrophic forgetting is limited), and sometimes it even helps with the new task. For example, both NMF-LTM and LCM achieve better NPMI scores with the latest KG in 'SIM Cards & Prepaid Minutes'". We are so sorry for the clerical error. The correct example should be "Pet Behavior Center", not "SIM Cards & Prepaid Minutes".
