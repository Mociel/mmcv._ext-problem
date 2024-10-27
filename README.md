## mmcv._ext problem
How to Solve No module named 'mmcv._ext' Error Report :)
### Warning: Date for this solution is SENSITIVE, as open-cd is evolving, updates may vary in the future.
### Date: 2024 Oct. 27

## Main installed package version
Open-CD: [v1.1.0](https://github.com/likyoo/open-cd/tree/v1.1.0)  
MMCV: [v2.2.0](https://mmcv.readthedocs.io/en/latest/get_started/installation.html)

# Environment：
Platform: Windows 11 23H2 22631.4317  
GPU:3060Ti  
CUDA_Ver:11.8
## Adopted(Changable) Environment:
Python version:3.10.0
Pytorch version: [2.3.0](https://pytorch.org/get-started/previous-versions/)
## Package versions
```
mmcv                   2.2.0  
mmdet                  3.3.0  
mmengine               0.10.5  
mmpretrain             1.2.0  
mmsegmentation         1.2.2  
numpy                  1.24.3  
opencd                 1.1.0  
opencv-python          4.10.0.84  
opendatalab            0.0.10  
openmim                0.3.9  
openxlab               0.1.2  
packaging              24.1  
setuptools             60.2.0  
torch                  2.3.0  
torchaudio             2.3.0  
torchvision            0.18.0  
```

# Fixs
When trying install GPU-version 'mmcv', [mmcv wheel](https://download.openmmlab.com/mmcv/dist/cu118/torch2.3/index.html)
can only accept correct version of CUDA and python.   
(To look for your desired version, simply try change the link with the following form:  
https://download.openmmlab.com/mmcv/dist/cu{CUDA_VERSION}/torch{TORCH_VERSION}/index.html  
example: https://download.openmmlab.com/mmcv/dist/cu118/torch2.3/index.html)  
Or refer to mmcv's installation doc.

1. Choose supported Python version and install mmcv supported PyTorch (You may need to downgrade your torch version as up to this date, mmcv not yet supporting torch2.4+11.8 wheel).  
2. Download directly the corresponding version of mmcv's wheel (/{torch_version}/{mmcv_version}-{cpython_version}-{python_version}-{platform}_x86_64.whl).  
3. Install this wheel:

```
pip install {your wheel file}
```
(e.g. mmcv-2.2.0-cp310-cp310-win_amd64.whl) 

Up to this point, the correct mmcv should then successfully installed.   
Incorrect version will cause following Error:  
```
ERROR: mmcv-2.2.0-cp310-cp310-win_amd64.whl is not a supported wheel on this platform.
```
## Version Incompatible issue

For some of the toolbox, they may as for certain specific version of mmcv, and wrong version may run into such error report:  
```
AssertionError: MMCV==2.2.0 is used but incompatible. Please install mmcv>=2.0.0rc4, <2.2.0.
```
Look into the traceback, you could find following similar path at the 2nd last error (example is for mmdet pack):  
```
\miniconda3\envs\cdmodel\lib\site-packages\mmdet\__init__.py
```
And here \_\_init\_\_.py spcifies the version in form as follows:
```
mmcv_minimum_version = '2.0.0rc4'
mmcv_maximum_version = '2.2.0'
mmcv_version = digit_version(mmcv.__version__)
```
You may consider change the version to get rid of the problem, or install v2.1.0 mmcv (Here I didn't find the wheels, if you found, kindly drop an issue so I could post here).  
One modification example:  
```
mmcv_minimum_version = '0.0.0'
mmcv_maximum_version = '9.9.0'
mmcv_version = digit_version(mmcv.__version__)
```
Then most things should work smoothly. For finding other issues and solutions, kindly leave an issue so that people could use mmcv easily and not struggling around websites.  
### Off you go and enjoy XD

