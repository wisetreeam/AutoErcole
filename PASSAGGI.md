# Tentativi configurazione progetto

### Passo 0: Installa Tensorflow 1.7.0 
Link: [https://www.gitclear.com/open_repos/tensorflow/tensorflow/release/v1.7.0](url))

Guida di riferimento da qui in poi: [https://medium.com/repro-repo/speed-up-learning-by-building-tensorflow-gpu-from-source-on-ubuntu-d03bb4e06b23](url)

La configurazione inizia installando tutte le dipendenze richieste nella prima parte della guida (con alcune modifiche di seguito riportate), ossia:
- Python 3.5 (3.6 untested but possible) - [https://www.python.org/downloads/release/python-360/](url)
- CUDA Toolkit 9.0 - [https://developer.nvidia.com/cuda-90-download-archive](url)
- cuDNN 7.0 - [https://developer.nvidia.com/rdp/cudnn-archive](url)
- CUDA Compute 6.1
- Ubuntu 16.04

Le modifiche da prendere in considerazione sono le seguenti:
- Ubuntu 22.04.3 LTS invece di Ubuntu 16.04, poiché per lavorare su Linux abbiamo scelto di usare un WSL (Windows Subsystem for Linux);
- Python 3.6 invece di Python 3.5, poiché JigsawCNN è stato testato su questa versione.

---
### Passo 1: Configura CUDA Toolkit 9.0
Segui la guida sottostante (reperibile a pagina 16 della [documentazione ufficiale](https://developer.download.nvidia.com/compute/cuda/9.0/Prod/docs/sidebar/CUDA_Quick_Start_Guide.pdf))

![image](https://github.com/wisetreeam/AutoErcole/assets/74073441/3192367b-f61a-4eac-8ef6-3c6a8823a9b5)

---
### Passo 2: Configura cuDNN 7.0
Segui la guida sottostante (reperibile a pagina 5 della [documentazione ufficiale](https://developer.download.nvidia.com/compute/machine-learning/cudnn/secure/v7.0.5/prod/Doc/cuDNN-Installation-Guide.pdf?wGjDYCK3g-itSJ2NbcHoD4J1_81wKT9ow0jOy7LXaMJR2THIKQ_82uM2Dq-lyPNcWX9jCBGJVbgZKrypdk8qxZKPDb3uZddAiWtXw1GW4K38wFsZfLfCvQCr4Z7hlo8Rpjkxlo8LZgx0H6FwQH84wqk4dj3R86B0aT3VVwooY3VTKMNuXDqGYxQXU2Qk2ZIjjA==&t=eyJscyI6ImdzZW8iLCJsc2QiOiJodHRwczovL3d3dy5nb29nbGUuY29tLyJ9)).

![image](https://github.com/wisetreeam/AutoErcole/assets/74073441/8d3bb1aa-2fe0-4057-a96a-d97327787b59)

---
### Passo 3: Installa Python 3.6.0

> Andremo ad installare Python 3.6.0 da sorgente

(3.1) Installa i pacchetti richiesti da Python con il seguente comando:
```bash
sudo apt-get install libbz2-dev libc6-dev libgdbm-dev libncursesw5-dev libreadline-gplv2-dev libssl-dev libsqlite3-dev tk-dev
```
(3.2) Installa Python dal link indicato nell'incipit della guida.
(3.3) Scompatta l'archivio .tgz con il seguente comando:
```bash
tar -zxvf python3.6.0.tgz
```
(3.4) Entra nella cartella appena estratta:
```bash
cd python3.6.1/
```
(3.5) Compila il codice
```bash
./configure
sudo make altinstall
```
### Passo 4: Proseguimento su guida precedentemente elencata