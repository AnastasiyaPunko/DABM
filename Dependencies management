# Dependencies management

## Theory

**What is Docker, and how it differs from dependencies management systems? From virtual machines?**

*Docker* is a set of platform as a service products that use OS-level virtualization to deliver software in packages called containers.
Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels.

*Dependency management systems* deal with packages - strictly formatted descriptions of libraries and/or binaries. 
A package typically declares: how to build/compile its content and where to store results; what dependencies are needed before and after installation; contacts and other metadata.

*Virtual machine* is the virtualization/emulation of a computer system. Virtual machines are based on computer architectures and provide functionality of a physical computer. 

1) The main difference between Docker and VMs lies in their *architecture*.VMs have the host OS and guest OS inside each VM. A guest OS can be any OS, like Linux or Windows, irrespective of the host OS. In contrast, Docker containers host on a single physical server with a host OS, which shares among them. Sharing the host OS between containers makes them light and increases the boot time. Docker containers are considered suitable to run multiple applications over a single OS kernel; whereas, virtual machines are needed if the applications or services required to run on different OS.<br>
2) Also Virtual Machines are stand-alone with their kernel and security features. Containers share the host kernel. The container technology has access to the kernel subsystems.<br>
3) VMs are isolated from their OS, and so they are not ported across multiple platforms without incurring compatibility issues. Docker container packages are self-contained and can run applications in any environment, and since they don’t need a guest OS, they can be easily ported across different platforms. Docker containers can be easily deployed in servers since containers being lightweight can be started and stopped in very less time compared to virtual machines.<br>
4) Virtual Machines are more resource-intensive than Docker containers as the virtual machines need to load the entire OS to start.

**What are the advantages and disadvantages of using containers over other approaches?**

*Advantages:*

*1) Portability.*<br>
As a part of a distributed system, containers are highly portable.
Because containers pack microservices and their dependencies in a small-sized package, it’s easy to move containers around.<br>
*2) Effective resource usage.*<br>
Code packaged within containers share most of the dependencies needed to run the containers, including an operating system, libraries, and frameworks.
There’s only one copy of necessary files in each hardware, leading to more effective resource usage. <br>
*3) Easier to maintain.*<br>
As containers use a microservices-based architecture, your code is broken down into manageable pieces that can be handled individually. <br>
*4) Highly Scalable.*<br>
Containerized applications are highly scalable, and they can scale up and down quickly by spinning up new nodes and/or pods when the needs call for it.

*Disadvantages:*

*1) Lacking Security measures.*<br>
Containers provide lightweight isolation from the host OS and containers within the same system. This leads to a weaker security boundary.<br>
*2) Runs only one OS.*<br>
This can be a benefit if you only use one OS, but if you need to be able to use it across different OS’s this is a negative.<br>

**Explain how Docker works: what are Dockerfiles, how are containers created, and how are they run and destroyed?**

*How Docker works*

Docker packages, provisions and runs containers. Container technology is available through the operating system: A container packages the application service or function with all of the libraries, configuration files, dependencies and other necessary parts and parameters to operate. Each container shares the services of one underlying operating system. Docker images contain all the dependencies needed to execute code inside a container, so containers that move between Docker environments with the same OS work with no changes.

Docker can build images automatically by reading the instructions from a *Dockerfile*. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.

*Creating the Container.*<br>
Go to the command line of your system. Use the command docker create plus any relevant options. This command creates a layer over the original image which is writeable and ready to run specific commands. This allows full manipulation of Docker images without running them, although once the user is satisfied with their amendments the image can be run so that it becomes a container. ( docker create [OPTIONS] IMAGE [COMMAND] [ARG...])

*Docker runs* processes in isolated containers. A container is a process which runs on a host. The host may be local or remote. When an operator executes docker run, the container process that runs is isolated in that it has its own file system, its own networking, and its own isolated process tree separate from the host. (docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...])

*Destroy Docker Containers.* <br>
Stop one or more running containers (docker stop [OPTIONS] CONTAINER [CONTAINER...]). 
Remove one or more containers (docker rm [OPTIONS] CONTAINER [CONTAINER...]).

**Name and describe at least one Docker competitor (i.e., a tool based on the same containerization technology).**

*Podman* is a popular container engine. A container engine is an all-in-one software that manages user requests, loads and verifies container images from a registry server, monitors, allocates, isolates system resources, and runs containers using a bundled container runtime. It allows users to handle and use containers by providing a user interface that abstracts the complexities involved in dealing with system security rules and policies. 
One significant difference between Docker and Podman is that the Podman starts containers as child processes. It also interacts directly with the registry and with the Linux Kernel using a runtime process. 
Podman does not require root access.
Additionally, Podman can run pods - collections containing one or more containers managed as a single entity and utilize a shared pool of resources.

**What is conda? How it differs from apt, yarn, and others?**

*Conda* is an open source package management system and environment management system. Conda quickly installs, runs and updates packages and their dependencies. Conda easily creates, saves, loads and switches between environments on your local computer. 

Conda can work locally.
It can work for each user independently and it does not require system administrator rights.

## Problem
### Anaconda

**Install conda**<br>
```python
!pip install -q condacolab
import condacolab
condacolab.install()
```
```python
!conda --version
```
**Create a new virtual environment**<br>
```python
!conda create -n myenvironment
```
Result:
```python
Collecting package metadata (current_repodata.json): done
Solving environment: done

## Package Plan ##
  environment location: /usr/local/envs/myenvironment

Preparing transaction: done
Verifying transaction: done
Executing transaction: done
#
# To activate this environment, use
#
#     $ conda activate myenvironment
#
# To deactivate an active environment, use
#
#     $ conda deactivate
```
```python
!activate myenvironment
```

**Install all necessary packages**<br>
```python
#Add necessary chanells
!conda config --add channels bioconda
!conda config --add channels conda-forge
!conda config --set channel_priority strict
```
```python
#Add necessary packages
!conda install -c bioconda fastqc=0.11.9
!conda install -c bioconda star=2.7.10b
!conda install -c bioconda samtools=1.16.1
!conda install -c bioconda picard
!conda install -c bioconda salmon=1.9.0
!conda install -c bioconda bedtools=2.30.0
!conda install -c bioconda multiqc=1.13
```
I've installed these tools through the Bioconda channel.<br>
The conda team packages a multitude of packages and provides them to all users free of charge in their default channel. But some packages are not included in the default channel. Therefore, there are other channels where packages are stored.<br>
For example, **Bioconda** lets you install thousands of software packages related to biomedical research using the conda package manager.
**Conda-forge** is a community channel made up of thousands of contributors. Conda-forge itself is analogous to PyPI but with a unified, automated build infrastructure and more peer review of recipes.

**Export and verify**<br>
```python
#Export the environment to the file 
!conda env export > myenvironment.yml
```
Result:
```python
name: myenvironment
channels:
  - conda-forge
  - bioconda
  - defaults
dependencies:
  - multiqc==1.13
  - fastqc==0.11.9
  - bedtools==2.30.0
  - salmon==1.9.0
  - samtools==1.16.1
  - star==2.7.10b
  - picard==2.18.29
  ```
```python
#Verify that the new environment was installed correctly
!conda env create -f myenvironment.yml
```

## Docker

**Install Docker**
```bash
#Uninstall old versions
sudo apt-get remove docker docker-engine docker.io containerd runc
```
Set up the repository
```bash
#Update the apt package index and install packages to allow apt to use a repository over HTTPS
sudo apt-get update

sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```
```bash
#Add Docker’s official GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```bash
#Use the following command to set up the repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
Install Docker
```bash
#Update the apt package index
sudo apt-get update
```
```bash
#Install Docker Engine, containerd, and Docker Compose
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

**Create a Dockerfile**
```bash
cd docker
```
```bash
#create file
touch Dockerfile
```
```bash
#Write all required dependencies
nano Dockerfile
```
Dockerfile: <br>
FROM ubuntu:22.04<br>

RUN apt-get update && apt-get install -y fastqc<br>
RUN apt-get update && apt-get install -y rna-star<br>
RUN apt-get update && apt-get install -y samtools<br>
RUN apt-get update && apt-get install -y picard<br>
RUN apt-get update && apt-get install -y salmon<br>
RUN apt-get update && apt-get install -y bedtools<br>
RUN apt-get update && apt-get install -y multiqc<br>


```bash
#Build Image
docker build -t test .
```
```bash
#Run Image
docker run --rm -it test
```

**Dockerfile after Hadolint**
```
FROM ubuntu:22.04

RUN apt-get update && apt-get install -y fastqc=0.11.9 --no-install-recommends  \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y rna-star=2.7.10b --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y samtools=1.16.1 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y picard=2.27.5 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y salmon=1.9.0 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y bedtools=2.30.0 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y multiqc=1.13 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
```
**Dockerfile with Labels**
```
FROM ubuntu:22.04

LABEL maintainer="anpunko@edu.hse.ru"
LABEL build_date="15-12-2022"
LABEL version="1.0"
LABEL description="Dependencies for RNA-seq analysis"

RUN apt-get update && apt-get install -y fastqc=0.11.9 --no-install-recommends  \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y rna-star=2.7.10b --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y samtools=1.16.1 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y picard=2.27.5 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y salmon=1.9.0 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y bedtools=2.30.0 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y multiqc=1.13 --no-install-recommends \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
```
