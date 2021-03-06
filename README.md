# iCAT - Isolated CAT

A docker container for [CogStack](https://cogstack.org/)/[MedCAT](https://github.com/CogStack/MedCAT)/[HuggingFace](https://huggingface.co/) development in isolated environments. This is meant for envs that are completely locked-out, everything has to be prebuilt and then moved. It contains the basic tools necessary to interact with the CogStack platform + GPU support + MedCAT + Transformers from HuggingFace.


### How to run [with GPU support]
0. Clone the repo and open the destination folder (or run `mkdir -p icat/models` folder for mounting)
1. To run (and download) the container do: 
```
docker run -t -d --name icat --hostname icat --user icat -p 8888:8888 --gpus all --mount type=bind,source="$(PWD)/icat/models",target=/home/icat/models --mount source=data,target=/data --mount source=projects,target=/home/icat/projects rattel/icat:latest zsh
```
2. If you do not want GPU support, remove the `--gpus all` and run
3. Connect to the container using `docker exec -it icat zsh`
4. Activate the environment `source /home/icat/.venv/play/bin/activate`
    * Jupyter: First set the password with `jupyter notebook password` and second, run using `nohup jupyter notebook --ip 0.0.0.0 &`. Now it will be available at `<server_ip>:8888`
5. If the container stops and you want to start it again, use: `docker start icat`


### How to Build 

1. Clone the repository
2. Run `docker-compose -f docker-compose-build.yml build`
3. Push to docker Hub or save to a file


### Current status

* Starts from a `pytorch/cuda` image
* Basic `ubuntu` packages pre-installed
* Configuration for `vim` and `zsh`
* Base python requirements for CogStack/MedCAT/HuggingFace pre-installed
* Volumes for data, models and projects
* Open ports for jupyter notebooks (8888)
* Pre-downloaded GPTv2 and BERT models


#### This is very experimantal
