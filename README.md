# JigsawNet

JigsawNet is an image fragment reassembly system based on convolutional neural network. It is able to robustly reassemble irregular shredded image fragments.

This repository includes CNN-based pairwise alignment measurement and loop-closure based global composition. Please check our published paper for more algorithm details (https://arxiv.org/pdf/1809.04137.pdf).

There are some of reassembly results from various public datasets and our own datasets (1st, 2nd, 3rd and 4th row contains 9, 36, 100, 376 piece fragments repectively). More results are demonstrated in our paper.

![demon](https://raw.githubusercontent.com/Lecanyu/JigsawNet/master/Examples/demo.png)





## 1. Prerequisites

We have tested this code on Windows10 x64 operation system.
We developed a CNN to measure pairwise compatibility, which has been implemented on Python 3.6 and tensorflow.
To globally reassemble, we designed a loop-based composition to calculate consistently reassembly result. The global algorithm has been implemented in C++ on Microsoft Visual Studio 2015 with CUDA 8 or 9 support. 

Below dependencies are necessary to run pairwise compatibility measurement module.
* Python 3.6
* Tensorflow 1.7.0 and its dependencies
> Versions history here: https://www.gitclear.com/open_repos/tensorflow/tensorflow/releases?page=7

You should install below software or libraries to run global reassembly part.
* OpenCV 3.4.1
* Eigen 3.3.4
* CUDA 8.0 or 9.0

Other version of those dependencies/libraries have not tested.

If you want to compile or run this code on different OS or environments, a few of modifications will be needed.

---
### Installazione dependencies - required versions

#### > CUDA 9.0 e cuDNN 7.0
Installiamo innanzitutto **CUDA Toolkit 9.0** dal seguente link: https://developer.nvidia.com/cuda-90-download-archive?target_os=Windows&target_arch=x86_64&target_version=10

Ad installazione completata procediamo scaricando **cuDNN 7.0** dal seguente archivio: https://developer.nvidia.com/rdp/cudnn-archive

> N.B.: Occorre avere un account *NVIDIA Developer* per effettuare il download.

Una volta installato anche cuDNN 7.0, andiamo a cercare la cartella in cui CUDA si è scaricato; provare a guardare su Program Files (per piattaforme Windows), ad esempio: `"C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v12.3"`.

Non appena questa è stata individuata aprire `"cudnn-9.0-windows10-x64-v7>cuda"` e copiare i file contenuti nelle cartelle `"bin"`, `"include"` e `"lib"` nelle corrispettive contenute in 
`"NVIDIA GPU Computing Toolkit\CUDA\v12.3"`.

#### > Bazel v0.10.0 e Tensorflow v1.7.0
Prima di installare Tensorflow 1.7.0 è necessario installare una sau dependency, **bazel**. Per farlo basta digitare quanto segue su terminale:

```console
choco install bazel --version 0.10.0-rc8 --pre -y
```
Una volta fatto è possibile scaricare Tensorflow v1.7.0 dal seguente link: https://github.com/tensorflow/tensorflow/releases/tag/v1.7.0


Apri la cartella ```tensorflow-1.7.0``` su VS Code e digita in console: 

```
python ./configure.py
``` 

Inizierà così il setup su console guidato di **tensorflow**:
``` 
$ python configure.py
WARNING: current bazel installation is not a release version.
Make sure you are running at least bazel 0.10.0
Please specify the location of python. [Default is C:\Python27\python.exe]: <ENTER>


Found possible Python library paths:
  C:\Python27\lib\site-packages
Please input the desired Python library path to use.  Default is [C:\Python27\lib\site-packages] <ENTER>

Do you wish to build TensorFlow with XLA JIT support? [y/N]: n
No XLA JIT support will be enabled for TensorFlow.

Do you wish to build TensorFlow with GDR support? [y/N]: n
No GDR support will be enabled for TensorFlow.

Do you wish to build TensorFlow with VERBS support? [y/N]: y
VERBS support will be enabled for TensorFlow.

Do you wish to build TensorFlow with CUDA support? [y/N]: y
CUDA support will be enabled for TensorFlow.

Please specify the CUDA SDK version you want to use, e.g. 7.0. [Leave empty to default to CUDA 9.0]: <ENTER>


Please specify the location where CUDA 9.0 toolkit is installed. Refer to README.md for more details. [Default is C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v12.3]: <ENTER>


Please specify the cuDNN version you want to use. [Leave empty to default to cuDNN 7.0]: <ENTER>


Please specify the location where cuDNN 7 library is installed. Refer to README.md for more details. [Default is C:/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v12.3]: <ENTER>


Please specify a list of comma-separated Cuda compute capabilities you want to build with.
You can find the compute capability of your device at: https://developer.nvidia.com/cuda-gpus.
Please note that each additional compute capability significantly increases your build time and binary size. [Default is: 3.5,5.2] <ENTER>


Do you wish to build TensorFlow with MPI support? [y/N]: n
No MPI support will be enabled for TensorFlow.

Please specify optimization flags to use during compilation when bazel option "--config=opt" is specified [Default is -march=native]: <ENTER>     


Would you like to interactively configure ./WORKSPACE for Android builds? [y/N]: n
Not configuring the WORKSPACE for Android builds.

Preconfigured Bazel build configs. You can use any of the below by adding "--config=<>" to your build command. See tools/bazel.rc for more 
details.
        --config=mkl            # Build with MKL support.
        --config=monolithic     # Config for mostly static monolithic build.
``` 

TO BE CONTINUED...

--- 

## 2. Run pairwise compatibility measurement

We provide three modes to drive the scripts. 

Training
------------
Train network on training dataset. Please read the code to make sure all of pathes are set correctly.
```
python boost.py -m training
```

batch_testing
------------
Test network performance on tfrecord. You should prepare the testing data before you run.
```
python boost.py -m batch_testing
```

single_testing
------------
Test network performance on image data. You just need to prepare the pairwise alignment file. The image merging will be done by our program.
```
python boost.py -m single_testing
```

We recommend you reading the code to figure out how to modify the path and tune whatever you want. We think the structure of code is relatively clear and it should be self-explanatory.

You can find data/file format demonstration in the 'Examples' folder.


## 3. Run global reassembly

Global reassembly module is developed in C++ with CUDA support. For the algorithm details, please check our paper.

You can find a running example (run.bat) in the 'Examples' folder. 
If you successfully compile this module, you can run the example data by following the corresponding data format.


## 4. Run the example data

Put your own compiled GlobalReassembly.exe into Examples folder, and then run the .bat file to reassembly.

If everything goes well, you will get several output files (filtered_alignments.txt, pose_result_x.txt, reassembled_result_x.png and selected_transformation.txt)

We have already put those output files into the folders for refering. 


## 5. Run your own datasets

To solve your own jigsaw puzzles, a pairwise alignment calculation module is needed. In our experiments, we use an [existing method](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.683.4733&rep=rep1&type=pdf) to calculate pairwise alignment candidates. But you can use other more fancy algorithms to do it.

The pairwise alignments are represented by a list of 3x3 rigid transformation matrix. Please check our example data for the format details.


## 6. Datasets and pre-trained net parameters
Our experiment datasets and pre-trained model can be downloaded [here](https://drive.google.com/open?id=1sUIcAzFTJNAAEEhqdYAKMKgzjVwRvsP4).

From this link, you can find 5 different datasets (one for training and four for testing) and the JigsawCNN parameters checkpoint which has been trained from the training dataset. 

You can directly load this checkpoint to run the example data. 

Note: For successfully load the checkpoint on your machine, you should modify the checkpoint file to correct path (i.e. JigsawCNN_checkpoint/g0/checkpoint, JigsawCNN_checkpoint/g1/checkpoint, ...). 
Since this code has been implemented on tensorflow, and the pretrained parameters can only be used on tensorflow library.




## 7. Citation
If our work is useful in your research, please cite 

```
@article{le2018jigsaw,
  title={JigsawNet: Shredded Image Reassembly using Convolutional Neural Network and Loop-based Composition},
  author={Le, Canyu and Li, Xin},
  journal={arXiv preprint arXiv:1809.04137},
  year={2018}
}
```
