# Deploy DaSiamRPN on Windows (64 bit), without GPU

## Copyright
Please notice this repository is credit to ``https://github.com/foolwood/DaSiamRPN`` and its developers. It contains some slight modifications based on ``https://github.com/foolwood/DaSiamRPN`` repository, making it suitable for Python 3, and Windows machine without GPU. 

## Prerequisite
Windows 64-bit system without GPU, Python 3.5 or higher 
Alarm: Windows 32-bit system and Windows 64-bit system with Python 2 doesn't support PyTorch. 

## Install Python on Windows
Go to Python's official Website and download executable installer for Python 3.5 or higher for Windows. You can simply click this: https://www.python.org/ftp/python/3.7.4/python-3.7.4-amd64.exe . Then follow the instruction to install it. 
After installing it, add the python to PATH. Open cmd and type: 
```
path=%path%;C:\Python 
```
If you installed Python on other directory, just replace the C:\Python with that directory. 

## Install packages 
### Install PyTorch
Open powershell and type the following commands to use Pip to install torch and torchvision. 
```
python -m pip install https://download.pytorch.org/whl/cpu/torch-1.1.0-cp37-cp37m-win_amd64.whl
python -m pip install https://download.pytorch.org/whl/cpu/torchvision-0.3.0-cp37-cp37m-win_amd64.whl
```

### Install numpy and opencv
Open powershell and type the following commands to use Pip to install numpy and opencv. 
```
python -m pip install opencv-python
```

## Download the source code and Pre-trained model
Open powershell in the directory you want the source code be placed in. And type: 
```
git clone https://github.com/zyouc518/DaSiamRPN
cd ./DaSiamRPN
```

Visit https://drive.google.com/drive/folders/1BtIkp5pB6aqePQGlMb2_Z7bfPy6XEj6H and download the ``SiamRPNBIG.model``, ``SiamRPNOTB.model``, and ``SiamRPNVOT.model``. Move them into ``DaSiamRPN/code/`` directory. 

## Download datasets
### Install utilities for smooth downloading 
Due to Windows doesn't have ``sed`` and ``wget`` commands, please visit GnuWin and download them. 
Click http://gnuwin32.sourceforge.net/downlinks/sed.php to download ``sed``. 
Click http://gnuwin32.sourceforge.net/downlinks/wget.php to download ``wget``. 
And add ``wget`` to PATH by opening a cmd and type: 
```
;%C:\Program Files (x86)\GnuWin32%\bin
```

### Download training data and groundtruth file
In the ``DaSiamRPN-master`` directory, open a powershell and type: 
```
cd code
mkdir OTB2015 
cd OTB2015
wget "http://cvlab.hanyang.ac.kr/tracker_benchmark/datasets.html"
cat datasets.html | findstr "\.zip" | sed -e 's/\.zip".*/.zip/' | sed -e s'/.*"//' >files.txt
cat files.txt | xargs -n 1 -P 8 -I {} wget -c "$baseurl/{}"
ls *.zip | xargs -n 1 unzip
rm -r __MACOSX/
cd ..
```
