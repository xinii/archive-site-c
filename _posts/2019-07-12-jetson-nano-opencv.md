---
title: How to Install OpenCV on NVIDIA Jetson Nano
tags: [OpenCV, NVIDIA, Jetson Nano, Install, Chinese]
style: fill
color: info
description: 在Jetson Nano上安裝OpenCV
---

## 生成swap文件

為防止編譯途中由於內存不足等問題報錯，
這裏首先提前創建壹個swap文件，存放路徑任意。
重啟後swap空間會消失，
以下編譯等全部工作完成後可以手動刪除這個文件。

```sh
$ fallocate -l 4G swapfile
$ chmod 600 swapfile
$ mkswap swapfile
$ sudo swapon swapfile
$ swapon -s
```

## 生成安裝腳本

[安裝OpenCV 4.0.0版本的腳本原始鏈接](https://github.com/AastaNV/JEP/blob/master/script/install_opencv4.0.0_Nano.sh)

以上是安裝OpenCV 4.0.0的版本，在這裏我們希望安裝較新的4.1.0版本，將上面的代碼稍作改動（版本號的部分）：

```sh
#!/bin/bash
#
# Copyright (c) 2018, NVIDIA CORPORATION.  All rights reserved.
#
# NVIDIA Corporation and its licensors retain all intellectual property
# and proprietary rights in and to this software, related documentation
# and any modifications thereto.  Any use, reproduction, disclosure or
# distribution of this software and related documentation without an express
# license agreement from NVIDIA Corporation is strictly prohibited.
#

if [ "$#" -ne 1 ]; then
    echo "Usage: $0 <Install Folder>"
    exit
fi
folder="$1"
user="nvidia"
passwd="nvidia"

echo "** Install requirement"
sudo apt-get update
sudo apt-get install -y build-essential cmake git libgtk2.0-dev pkg-config libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install -y libgstreamer1.0-dev libgstreamer-plugins-base1.0-dev
sudo apt-get install -y python2.7-dev python3.6-dev python-dev python-numpy python3-numpy
sudo apt-get install -y libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff-dev libjasper-dev libdc1394-22-dev
sudo apt-get install -y libv4l-dev v4l-utils qv4l2 v4l2ucp
sudo apt-get install -y curl
sudo apt-get update

echo "** Download opencv-4.1.0"
cd $folder
curl -L https://github.com/opencv/opencv/archive/4.1.0.zip -o opencv-4.1.0.zip
curl -L https://github.com/opencv/opencv_contrib/archive/4.1.0.zip -o opencv_contrib-4.1.0.zip
unzip opencv-4.1.0.zip 
unzip opencv_contrib-4.1.0.zip 
cd opencv-4.1.0/

echo "** Building..."
mkdir release
cd release/
cmake -D WITH_CUDA=ON -D CUDA_ARCH_BIN="5.3" -D CUDA_ARCH_PTX="" -D OPENCV_EXTRA_MODULES_PATH=../../opencv_contrib-4.1.0/modules -D WITH_GSTREAMER=ON -D WITH_LIBV4L=ON -D BUILD_opencv_python2=ON -D BUILD_opencv_python3=ON -D BUILD_TESTS=OFF -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local ..

make -j3
sudo make install
sudo apt-get install -y python-opencv python3-opencv

echo "** Install opencv-4.1.0 successfully"
echo "** Bye :)"
```

將上面的腳本保存為`sh`文件，例如`install_opencv4.1.0_Nano.sh`。

## 運行腳本

```sh
mkdir opencv
sh install_opencv4.1.0_Nano.sh opencv
```
安裝會比較花時間，耐心等待安裝結束，建議使用tmux等掛在後臺執行。


## 測試安裝好的OpenCV

通過python的交互界面測試語句`import cv2`，不報錯則安裝完成。

不過，考慮到使用pyenv等工具進行python版本管理的用戶，
此時如果切換到pyenv下安裝的python版本可能無法檢測到已安裝的OpenCV，
作為解決版本是創建壹個OpenCV庫的軟鏈接到pyenv中python版本的庫目錄下。

假設妳的pyenv中的python版本的庫目錄為
`/home/xin/.anyenv/envs/pyenv/versions/3.6.8/lib/python3.6/site-packages`，
安裝好的OpenCV庫路徑為
`/usr/local/lib/python3.6/dist-packages/cv2/python-3.6/cv2.cpython-36m-aarch64-linux-gnu.so`，
那麽執行下面的語句即可創建軟鏈接。

```sh
cd /home/xin/.anyenv/envs/pyenv/versions/3.6.8/lib/python3.6/site-packages
ln -s /usr/local/lib/python3.6/dist-packages/cv2/python-3.6/cv2.cpython-36m-aarch64-linux-gnu.so ./
```

另外提前使用pyenv中的python版本的pip通過
`pip install numpy`語句安裝好numpy，
去交互界面測試`import cv2`無錯誤顯示則安裝完成。
