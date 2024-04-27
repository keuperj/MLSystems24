# Exercise 1: Anaconda Environments
* boot a linux base system and start a terminal
* pull and start a *anaconda* docker container:
```
docker run -t -i continuumio/miniconda3 /bin/bash
```
* check *conda* environment:
```
conda info
```

## Links:
* [Anaconda User Guide](https://docs.conda.io/projects/conda/en/latest/user-guide/index.html)
* [Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/a35958a2a7fa1e927e7dfb61ebcd69a9/conda-4.14.pdf)

## Task 1
* setup a new environment named *project1* and switch to this environment
* install *numpy* with version 1.24.3
* install *scipy* and scikit-learn
* clone the environment to *project2* and install the latest version of numpy
* export the environment for deployment

## Task 2
* end the docker container (type ```exit``` in container terminal) and get a new one:
```
docker run -p 10000:8888 jupyter/scipy-notebook:2023-02-28
```
* open the jupyter environment in your browser
* open the jupyter terminal and start a new conda environment *project3*
* create and use a new Jupyter kernel with this environment ([see docu](http://echrislynch.com/2019/02/01/adding-an-environment-to-jupyter-notebooks/))
