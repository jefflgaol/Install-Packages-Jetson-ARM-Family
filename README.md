# Install-Packages-Jetson-ARM Family
The objective is to give you clear instructions on how to install packages in ARM platform primarily in Jetson family. This instruction was made for Python 3. Tests have been made on Jetson TX2 and Jetson Xavier. You may change ```sudo python3``` and ```sudo pip3``` to ```sudo python2``` and ```sudo pip``` respectively to make it work with Python 2.

## Dependencies Installation
Before performing any installations, you may need to install the basic dependencies first.
```
$ sudo apt-get install cmake
$ sudo apt-get install python3-pip
$ sudo pip3 install wget
```

## PyCUDA Installation
```
$ sudo apt-get install libboost-all-dev
$ sudo apt-get install python-numpy
$ sudo apt-get install build-essential python-dev python-setuptools libboost-python-dev libboost-thread-dev
```
You need to download PyCUDA from https://pypi.org/project/pycuda/#files. In the same directory of your download, run this terminal
```
tar xzvf pycuda-VERSION.tar.gz
cd pycuda-VERSION
./configure.py
make -j4
sudo python3 setup.py install
sudo pip3 install .
```

## LLVM Installation
In this tutorial, I used LLVM 7.0.1.
```
$ wget http://releases.llvm.org/7.0.1/llvm-7.0.1.src.tar.xz
$ tar -xvf llvm-7.0.1.src.tar.xz
$ cd llvm-7.0.1.src
$ mkdir llvm_build_dir
$ cd llvm_build_dir/
$ cmake ../ -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD="ARM;X86;AArch64"
$ make -j4
$ sudo make install
$ cd bin/
$ echo "export LLVM_CONFIG=\""`pwd`"/llvm-config\"" >> ~/.bashrc
$ echo "alias llvm='"`pwd`"/llvm-lit'" >> ~/.bashrc
$ source ~/.bashrc
$ sudo pip3 install llvmlite
```

## Numba Installation
Before proceeding to the Numba installation, you need to perform LLVM installation above first since Numba is heavily rely on LLVM installation.
```
sudo pip3 install numba
```

## Protobuf Installation
You may install Protobuf directly from Python using pip:
```
sudo pip3 install protobuf
```
If that doesn't work, you may build from source:
```
$ git clone https://github.com/protocolbuffers/protobuf.git
$ cd protobuf
$ git submodule update --init --recursive
$ ./autogen.sh
$ ./configure
$ make
$ make check
$ sudo make install
$ sudo ldconfig
```

## ONNX Installation
Before proceeding to the ONNX installation, you need to perform Protobuf installation above first since ONNX heavily relies on Protobuf installation.
```
$ sudo pip3 install onnx
```

## Keras Installation
```
$ sudo apt-get install libblas-dev liblapack-dev libatlas-base-dev gfortran
$ sudo pip3 install scipy
$ sudo pip3 install keras
```

## Tensorflow Installation
```
$ sudo apt-get install libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev
$ sudo pip3 install -U numpy==1.16.1 future==0.17.1 mock==3.0.5 h5py==2.9.0 keras_preprocessing==1.0.5 keras_applications==1.0.6 enum34 futures testresources setuptools protobuf
```
If you have trouble installing Protobuf, you may take a look at the Protobuf installation part above. If everything's fine, you may proceed. Now, take a look at this https://developer.download.nvidia.com/compute/redist/jp/. You may find a lot of JetPack versions and you need to choose one based on your preference. In this tutorial, I used v33 since it has compatibility with Python 2 installation. 
```
sudo pip3 install --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v33 tensorflow-gpu
```
