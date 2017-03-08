### Introduction

[README.md](https://github.com/OneDirection9/py-faster-rcnn/blob/master/README.md) may not be so helpful when you try to run py-faster-rcnn on windows, so I write down my installation process. Hope to help beginners.

# py-faster-rcnn on windows

You can see my environment on the top of [README.md](https://github.com/OneDirection9/py-faster-rcnn/blob/master/README.md).

I refer the [caffe installation](http://www.cnblogs.com/LaplaceAkuir/p/6445189.html) and [windows py-faster-rcnn config](http://www.cnblogs.com/LaplaceAkuir/p/6484500.html).

### Contents

1. [Cudnn installation](#Cudnn-installation)
2. [Caffe installation](#Caffe-installation)
3. [Faster rcnn installation](#py-faster-rcnn-installation)
4. [Demo](#Demo)
5. [Problems and solutions](#Problems-and-solutions)

### Cudnn installation

Download the [zip](https://developer.nvidia.com/rdp/cudnn-download) and extract it. Then copy the files to corresponding location in `C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v7.5`.
If you do that, you don't need to add `$Cudnn_PATH` to environment variables.

### Caffe installation

I use the [Microsoft caffe](https://github.com/Microsoft/caffe) and assume that you have installed VS2013, CUDA7.5, and e.g.

1. Clone `caffe` from github

  ```make
  # recommond u to use --recursive
  git clone --recursive https://github.com/Microsoft/caffe.git
  ```

2. Copy `caffe/windows/CommonSettings.props.example` to `caffe/windows/CommonSettings.props`

   Modify `caffe/windows/CommonSetting.props` with sublime or other text editor. You can refer to the [Microsoft caffe README.md](https://github.com/Microsoft/caffe/blob/master/README.md) for details.

3. Install packages
  
  Install some python dependency packages.
  ```make
  conda install --yes numpy scipy matplotlib scikit-image pip
  pip install protobuf
  ```
  
4. Config faster-rcnn

   Due to the use of `roi_pooling_layer` in `faster-rcnn`, we need to add `.hpp`, `.cu`, and `.cpp` files to the `libcaffe`. Then rebuild the whole Solution and wait for the end of compile.
  
   - set PythonPath environment variable to point to `<caffe_root>\Build\x64\Release\pycaffe`, or
   - copy folder `<caffe_root>\Build\x64\Release\pycaffe\caffe` under `<python_root>\lib\site-packages`.
   
   Otherwise you may meet: No module named caffe.
   
### Faster rcnn installation

1. Clone `py-faster-rcnn` from github
  
  ```make
  # recommond u use --recursive
  # because the py-faster-rcnn repository has a submodules.
  git clone --recursive https://github.com/rbgirshick/py-faster-rcnn
  ```
  
2. Clone `lib` from github

   Download the lib and replace it with the original lib provied by rbgirshick.
  ```make
  git clone https://github.com/MrGF/py-faster-rcnn-windows
  ```
  
3. Copy `caffe` to `py-faster-rcnn`
   
   Copy files under `<caffe_root>\Build\zx64\Release\pycaffe\` you have built to `<py-faster-rcnn_root>\caffe-fast-rcnn\python\`.

4. Install depency packages

  ```make
  conda install numpy pyqt
  ```
  
5. Run
   
  ```make
  cd <py-faster-rcnn_root>\lib\
  python setup.py install
  ```
   
   Modify the cuda path in line 33 setup_cuda.py file.
  ```make
  python setup_cuda.py install
  ```
  
### Demo

To run demo you need download prebuild models.

### Problems and solutions