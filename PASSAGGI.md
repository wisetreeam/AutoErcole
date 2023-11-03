# Tentativi configurazione progetto
Guida di riferimento: [https://medium.com/repro-repo/speed-up-learning-by-building-tensorflow-gpu-from-source-on-ubuntu-d03bb4e06b23](url)

### Passo 0: Installa Tensorflow 1.7.0 
Link: [https://www.gitclear.com/open_repos/tensorflow/tensorflow/release/v1.7.0](url))
Per buildare Tensorflow occorre aver installato Bazel; per ottenerlo, digitare il seguente comando su Command Prompt di Windows:
```choco install bazel --version 0.10.0-rc8 --pre -y```

La configurazione inizia installando tutte le dipendenze richieste nella prima parte della guida (con alcune modifiche di seguito riportate), ossia:
- Python 3.5 (3.6 untested but possible) - [https://www.python.org/downloads/release/python-360/](url)
- CUDA Toolkit 9.0 - [https://developer.nvidia.com/cuda-90-download-archive](url)
- cuDNN 7.0 - [https://developer.nvidia.com/rdp/cudnn-archive](url)
- CUDA Compute 6.1
- Ubuntu 16.04

Le modifiche da prendere in considerazione sono le seguenti:
- Ubuntu 22.04.3 LTS invece di Ubuntu 16.04, poiché per lavorare su Linux abbiamo scelto di usare un WSL (Windows Subsystem for Linux);
- Python 3.6 invece di Python 3.5, poiché JigsawCNN è stato testato su questa versione.

### Passo 1: Configura CUDA Toolkit 9.0
Segui la guida sottostante (reperibile a pagina 16 della [documentazione ufficiale]([url](https://developer.download.nvidia.com/compute/cuda/9.0/Prod/docs/sidebar/CUDA_Quick_Start_Guide.pdf)))
![image](https://github.com/wisetreeam/AutoErcole/assets/74073441/3192367b-f61a-4eac-8ef6-3c6a8823a9b5)
