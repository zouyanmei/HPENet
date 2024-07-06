# BAFM-and-MAL
Official PyTorch implementation for the following paper:

**Fine-grained Semantic Information Preservation and Misclassification-aware Loss for 3D Point Cloud**

*by Yanmei Zou, Xuefei Lin, [Hongshan Yu](http://eeit.hnu.edu.cn/info/1289/4535.htm) *, [Zhengeng Yang](https://gsy.hunnu.edu.cn/info/1071/3537.htm), [Naveed Akhtar](https://findanexpert.unimelb.edu.au/profile/1050019-naveed-akhtar)

## Features
In the project, we propose:
1. a plug-and-play bilateral attention fusion module (BAFM) to improve the performance of “Encoder-Decoder” structures by preserving fine-grained semantic information for dense multi-classification tasks.

2. a misclassification-aware loss (MAL) function to fully exploit the predicted information by applying a more informed penalty on the misclassified classes.

3. We extend MAL as a novel post-processing operation to improve the performance of existing techniques.



## Installation

```
git clone git@github.com:zouyanmei/BAFM-and-MAL.git
cd BAFM-and-MAL
source install.sh
```
Note:  

1) the `install.sh` requires CUDA 11.1; if another version of CUDA is used,  `install.sh` has to be modified accordingly; check your CUDA version by: `nvcc --version` before using the bash file;
2) you might need to read the `install.rst` for a step-by-step installation if the bash file (`install.sh`) does not work for you by any chance;
3) for all experiments, we use wandb for online logging by default. Run `wandb --login` only at the first time in a new machine, or set `wandn.use_wandb=False` if you do not want to use wandb. Read the [official wandb documentation](https://docs.wandb.ai/quickstart) if needed.



## Usage 

**Check `README.md` file under `cfgs` directory for detailed training and evaluation on each benchmark.**  

For example, 
* Train and validate on ScanObjectNN for 3D object classification, check [`cfgs/scanobjectnn/README.md`](cfgs/scanobjectnn/README.md)
* Train and validate on ModelNet40 for 3D object classification, check [`cfgs/modelnet40ply2048/README.md`](cfgs/modelnet40ply2048/README.md)
* Train and validate on S3DIS for 3D segmentation, check [`cfgs/s3dis/README.md`](cfgs/s3dis/README.md)

Note:  
1. We use *yaml* to support training and validation using different models on different datasets. Just use `.yaml` file accordingly. For example, train on ScanObjectNN using PointNeXt: `CUDA_VISIBLE_DEVICES=1 bash script/main_classification.sh cfgs/scanobjectnn/pointnext-s.yaml`, train on S3DIS using ASSANet-L: `CUDA_VISIBLE_DEVICES=1 bash script/main_segmentation.sh cfgs/s3dis/assanet-l.yaml`.  
2. Check the default arguments of each .yaml file. You can overwrite them simply through the command line. E.g. overwrite the batch size, just appending `batch_size=32` or `--batch_size 32`.  


## Model Zoo

We provide the **training logs & pretrained models** in column `our released`  *trained with the improved training strategies proposed by our methods through Google Drive. 

### ScanObjectNN (Hardest variant) Classification


|       name           |    mAcc / OA     |                 Param.(M)                  | FLOPs(G)
| :-------------------: | :----------------------------: | :----------------------------------------------------------: | :----------------------------:
| PointMLP-elite*      | 82.1 / 83.7 |                    0.7   |  1.8
| Our (PointMLP-elite) | 82.3 / 84.2                    |   0.7   |  1.8
| PointMLP-elite(Orig) | 81.7  / 84.1  | 0.7 | 1.8
| Our (PointMLP-elite(Orig))        | 82.0 / 84.1 | 0.7 | 1.8
| PointMLP(Orig)     | 84.4 / 86.1  | 13.2  | 31.4
| Our (PointMLP(Orig))  |  84.8 / 86.4 | 13.2 | 31.4           
| PointNeXt-S*  | 85.5 / 87.8  | 1.4 | 1.6     
| Our (PointNeXt-S*)  | 86.4 / 87.8 | 1.4 | 1.6     
| PointNeXt-S(Orig) | [86.8 / 88.2](https://drive.google.com/drive/folders/1A584C9x5uAqppbjNNiVqlA_7uOOOlEII?usp=sharing) | 1.4 | 1.6  
| **Our(PointNeXt-S(Orig))** | **87.0 / 88.4** | 1.4 | 1.6




### S3DIS (Area 5) Segmentation

|       name             |    mIoU /OA /mAcc (Original)                 
| :--------------:       | :----------------------------: 
|    	PointNeXt-XL*      |      70.2 / 76.0 / 90.7           
|    	Our (PointNeXt-XL) |      [71.3 / 77.2 / 90.3](https://drive.google.com/drive/folders/130hZ4FmVsITNSdRQocYeQtHcdJCAyxFS)   






### ModelNet40 Classificaiton

|       name           |   OA / mAcc     |                 Param.(M)             
| :-------------------: | :----------------------------: | :----------------------------------------------------------:
| CurveNet*            | 93.5 / 90.4 |2.0
| Our (CurveNet)       | [93.8 / 90.8](https://drive.google.com/drive/folders/1OfFhO6aMcyJFG6ZgpyhxLns9X1KvSExs) | 2.0
| CurveNet(Orig)       | [93.8 / 91.1](https://drive.google.com/drive/folders/1fRk631bn8ddfijm0auZN47DwY8ERjfUl) | 2.0
| Our (CurveNet(Orig)) | [94.0 / 91.4](https://drive.google.com/drive/folders/1_dVmkNlspc8_XAEq69L5IvfoyF8kU3t7) | 2.0
| PointMLP-elite*      | 92.9 / 90.2 | 0.7
| Our (PointMLP-elite) | 93.3 / 90.4 | 0.7
| PointMLP(Orig)       | [94.1 / 91.3](https://drive.google.com/drive/folders/1zLzdibmWPfy8igjH61gsfHIOqQuDUqpL) | 13.2
| Our (PointMLP(Orig)) | **94.1 / 91.9** | 13.2




