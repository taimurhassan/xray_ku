# A learned framework for detecting suspicious item in X-ray security imagery
This repository contains the source code for detecting suspicious items in security X-ray scans using novel Graph Representational Learning approaches. This work is developed by RISETech Private Limited, Pakistan for Khalifa University, UAE.

![Block_Diagram](images/ku.png)


## Requirements
This codebase is developed and fully tested on Anaconda with **Python 3.6.10**, **Pytorch 1.5.0** with **CUDA 10.1** on **Ubuntu v20.04**. Hence, we recommend the utilization of the same execution environment in order to avoid any setup errors. Also, please note that we do not support Windows OS. 

The code flow is currently dependent on two virtual environments, i.e., `cellGraph.yaml` and `metrics.yaml`. `cellGraph.yaml` is to be used for training and testing the proposed framework. Moreover, in order to fairly compare our work with state-of-the-art, `metrics.yaml` environment has to be used, as it computes the crc metrics originally developed by the [HoVerNet](https://github.com/vqdang/hover_net) devs. In future, we will merge both of these two environments. But, for now, we recommend their independent usage just to avoid libs incompatibility.   

## Setup

1. Import the 'cellGraph.yaml' and install the related code dependencies as:
    1. `conda env create -f cellGraph.yaml`
    2. `conda activate cellGraph`

2. Import the 'metrics.yaml' and infer the related libraries from the 'requirement.txt' file:
   1. `conda env create -f metrics.yaml`
    
3. Download the CRC datasets from their respective link, convert the dataset using `datasetConverter.m` script. Place the converted dataset in the `data` folder within project's root directory.

4. Create an `output` folder within root directory to save proposed framework's output. 

## Training
1. After placing the desired dataset in the `data` folder. Please make sure that the following dataset configurations are updated:
   1. 'sequence_numbers' in `seq_processor.py`
   2. 'frame_numbers' in `splits.py`

2. Train the proposed framework by running:
```
python scripts/train.py 
```
By default, HoVer-Net is chosen as a backbone detector. If you want to use Faster R-CNN, then please run:
```
python scripts/train.py with prepr_w_tracktor=False
```

## Inference
1. In order to evaluate the proposed framework on the test dataset, please run:
```
python scripts/evaluate.py 
```
or
```
python scripts/evaluate.py with prepr_w_tracktor=False
```
2. To compute performance metrics, please activate `metrics.yaml` in a seperate shell, and run:
```
python compute_stats.py --mode=type --pred_dir='pred_dir' --true_dir='true_dir'
```

## Note
If you use any part of this code, then please take prior permission from Khalifa University, UAE by emailing to: naoufel.werghi@ku.ac.ae

