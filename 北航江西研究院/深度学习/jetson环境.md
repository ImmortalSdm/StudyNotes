
安装Miniforge
```
bash Miniforge3-Linux-aarch64.sh
```

```
conda create --name FairMOT python=3.6
```

```
source activate FairMOT
```

```
which pip

```

pytorch
```
pip install 'torch-1.2.0a0+8554416-cp36-cp36m-linux_aarch64.whl'
```

wei
```
git clone https://github.com/pytorch/vision.git
cd vision
git checkout -b v0.4.0
python setup.py install #wuxiao
```

```
pip install torchvision
```

```
cd  ~/FairMOT
pip3 install -r requirements.txt
```

```
sudo apt-get install libtinfo-dev
pip install llvmlite==0.34.0
pip3 install numba==0.31
```