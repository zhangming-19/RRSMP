# SMPRR
This repository releases a comprehensive dataset for long-term stock movement prediction from Chinese research reports and historical stock prices. We will open source all data and code in the near future. Please cite the following [paper](https://www.sciencedirect.com/science/article/pii/S0957417422014427) if you use this dataset.

> Stock movement prediction is a challenging problem: the market is highly *stochastic*, and we make *long-term* predictions from *chaotic* data. We treat these three complexities and present a novel long-term stock movement prediction approach based on research reports. In detail, a new Research Report dataset for Stock Movement Prediction (SMPRR) is proposed. SMPRR is one of the few datasets for long-term stock movement prediction, which is mainly composed of long-form, formal, and professional research reports. We demonstrate the state-of-the-art performance of our proposed model on SMPRR.

<!--You might also be interested in our code for stock movement prediction. We have deposited the code in the Code Ocean platform. The accepted code capsules can be found through https://codeocean.com/capsule/8892872/tree/v1. The DOI of the code is https://doi.org/10.24433/CO.2855516.v1
-->

Should you have any query please contact me at [zhangming@hccl.ioa.ac.cn](mailto:zhangming@hccl.ioa.ac.cn).

## Dataset Overview
The research reports between 07/23/2009 and 03/02/2022 are downloaded from the Eastmoney.com, which are publicly available on the web. Correspondingly, the historical prices of related stocks are obtained from the public finance [API](https://tushare.pro/) for the last ten years.

## Data Component
This dataset comprises two main components,

* **./reports**: textual data from [reasearch reports](https://data.eastmoney.com/)
* **./price**: price data from finance [API](https://tushare.pro/)

Each component contains their raw data, preprocessed data, and finished data organized by year,

* **./reports/Raw**
* **./reports/Pre**
* **./reports/Finished**
* **./reports/Modules**

and

* **./price**

## Data Format

### Raw Research Report Data
Format: PDF

Keys: see more in the [Eastmoney.com](https://data.eastmoney.com/)

### Preprocessed Research Report Data
Format: XLS

Keys: 'Title', 'Links', 'Org.', 'Author', 'Rate', 'Date', 'Text'

### Finished Research Report Data
Format: CSV

Keys: 'id', 'text', 'category', 'rating'

### Modules Research Report Data
Format: CSV 

Keys: 'id', 'text', 'category', 'rating'

### Raw Price Data
Format: CSV 

Keys: 'Date', 'Open', 'Close', 'High', 'Low', 'Volume', 'Amount', 'Amplitude', 'Quote_change', 'Mount_change' and 'Turnover_rate'

## Codes
### Requirements
We use Conda python 3.7 and strongly recommend that you create a new environment.

conda create -n bart python=3.7.

### Environment
* Python 3.7
* PyTorch 1.4.0+cu100
* HuggingFace Transformers 4.16.2
* boto3 1.24.32
* numpy 1.21.4
* pandas 1.1.5
* regex 2022.7.9
* sentencepiece 0.1.96
* sklearn latest


 ### Prepare data 
 You can get data here (https://github.com/zhangming-19/SMPRR). Put them under the dir data/*.
* bash ./Step01_process.sh

################################

### Reproduce Results 

################################

You can follow the following steps to reproduce the best results in our paper.

### Download checkpoints 
 Download checkpoints (Ours_FinBert_360_Ex2019_part0X_GRU_X) here (https://github.com/zhangming-19/SMPRR). Put the checkpoints under the dir data/*.

### Inference 
 Since there is only one '/data' folder, you need to infer part01 to part04 sequentially. In detail, you need to configure inference data in Step01_process.sh, and then infer.

* bash ./Step05_eval_dev_part01.sh
* bash ./Step05_eval_dev_part02.sh
* bash ./Step05_eval_dev_part03.sh
* bash ./Step05_eval_dev_part04.sh

### Combine 
* bash ./Step06_combine_dev_FinBert.sh

### Analysis 
* bash ./Step07_analysis_dev_FinBert.sh

### MFF-FinBERT 
* bash ./Step08_MFF_result.sh

################################

### From Scratch 

################################

### Download FinBERT checkpoint
 Download finbart.base checkpoint (https://github.com/zhangming-19/SMPRR). Put it under the dir ./chinese_finbert_base_pytorch/*.

### Train and infer 
 Since there is only one '/data' folder, you need to infer part01 to part04 sequentially. In detail, you need to configure inference data in Step01_process.sh, and then infer.

* bash ./Step02_run_FinBert_part01.sh
* bash ./Step02_run_FinBert_part02.sh
* bash ./Step02_run_FinBert_part03.sh
* bash ./Step02_run_FinBert_part04.sh

### Combine 
* bash ./Step03_combine_FinBert.sh

### Analysis 
* bash ./Step04_analysis_result_FinBert.sh

### MFF-FinBERT 
* bash ./Step08_MFF_result.sh

## Citation
@article{ZHANG2022118312,  
title = {Predicting long-term stock movements with fused textual features of Chinese research reports},  
journal = {Expert Systems with Applications},  
volume = {210},  
pages = {118312},  
year = {2022},  
issn = {0957-4174},  
doi = {https://doi.org/10.1016/j.eswa.2022.118312},  
url = {https://www.sciencedirect.com/science/article/pii/S0957417422014427},  
author = {Ming Zhang and Jiahao Yang and Meilin Wan and Xuejun Zhang and Jun Zhou},  
keywords = {Long-term stock prediction, Research report, Financial text mining, Textual feature, Pre-trained language model},  
abstract = {By shaping investors’ perceptions and assessments of the stock, research reports have significant impacts on the stock market. Due to the limitations of text mining technology, it is difficult for researchers to effectively utilize long research reports, and most studies mainly focus on investor sentiment. However, due to the lack of appropriate open-domain toolkits, the annotations of sentiment often require expensive manual labeling. In addition, most existing studies have shown the success of using textual data as a supplement to historical price data in short-term forecasting, but not in long-term forecasting. To cover this gap and solve the problem of difficult annotations, we introduce a novel knowledge-driven approach for long-term stock movement prediction based on Chinese research reports. In detail, a new long-term Stock Movement Prediction dataset composed of Research Reports is proposed, namely SMPRR. It is mainly composed of long, formal, and professional research reports and historical prices. Furthermore, we propose the Multi-module Feature Fusion method based on the pre-trained language model FinBERT (MFF-FinBERT), which can effectively fuse textual features from research reports. The experiment results show that the proposed model has achieved better performance than existing methods in the forecasting of one-year stock movements, and the accuracy reaches 79.2%. The results also indicate that the basic information of stocks plays an important role in long-term forecasting, which is in line with the theory of value investing.}
}






