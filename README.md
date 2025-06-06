# HPENet
Official PyTorch implementation for the following paper, which was accepted by AAAI2024:

**Improved MLP Point Cloud Processing with High-Dimensional Positional Encoding**

*by [Yanmei Zou](https://orcid.org/my-orcid?orcid=0000-0002-9102-8724), [Hongshan Yu](http://eeit.hnu.edu.cn/info/1289/4535.htm) *, [Zhengeng Yang](https://gsy.hunnu.edu.cn/info/1071/3537.htm), Zechuan Li, [Naveed Akhtar](https://findanexpert.unimelb.edu.au/profile/1050019-naveed-akhtar)

We extend HPENet to HPENet V2, please refer to [https://github.com/zouyanmei/HPENet_v2](https://github.com/zouyanmei/HPENet_v2) for details.

## Features
In the project, 
1. We identify a unified “abstraction and refinement” paradigm underpinning the current high-performing point cloud modeling techniques, which allows an intuitive  delineation of the key strengths of the methods.
2. We propose a High-dimensional Positional Encoding (HPE) scheme for effective point cloud geometric representation with positional information. The HPE scheme can be generically used to enhance MLP architectures.
3. We propose HPENets, which are ABS-REF stage inspired MLP networks that leverages our HPE modules in both ABS and REF stages.
4. With an extensive evaluation of our technique, we establish state-of-the-art (SOTA) results of 87.6 mAcc on ScanObjectNN for object classification, 85.5 class mIoU on ShapeNetPart for object part segmentation, and 72.7 and 78.7 mIoU on Area-5 and 6-fold experiments with S3DIS for semantic segmentation.



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




### S3DIS Segmentation

|       name             |    mIoU /OA /mAcc (Original)                 
| :--------------:       | :----------------------------: 
|    	PointNeXt-XL*      |      70.2 / 76.0 / 90.7           
|    	Our (PointNeXt-XL) |      [71.3 / 77.2 / 90.3](https://drive.google.com/drive/folders/130hZ4FmVsITNSdRQocYeQtHcdJCAyxFS)   










