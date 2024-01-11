# DABM
Master’s Programme Data Analysis in Biology and Medicine

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



# Working with remote servers
## Theory

**What are computer ports on a high level? How many ports are there on a typical computer?**<br>
A port is a virtual point where network connections start and end. Ports are software-based and managed by a computer's operating system. Each port is associated with a specific process or service. Ports allow computers to easily differentiate between different kinds of traffic.<br>
There are 65,535 possible port numbers. Port numbers have three ranges: System Ports (0-1023), User Ports (1024-49151), and the Dynamic and/or Private Ports (49152-65535).<br>

**What is the difference between http, https, ssh, and other protocols? In what sense are they similar? Name default ports for several data transfer protocols.**<br>
HTTP: The Hypertext Transfer Protocol (HTTP) is used for transferring data between devices. HTTP belongs to the application layer (layer 7), because it puts data into a format that applications can use directly, without further interpretation. The lower layers of the OSI model are handled by a computer's operating system, not applications.<br>
HTTPS: The problem with HTTP is that it is not encrypted — any attacker who intercepts an HTTP message can read it. HTTPS corrects this by encrypting HTTP messages.<br>
SSH means “Secure Shell”. It has a built-in username/password authentication system to establish a connection. It uses Port 22 to perform the negotiation or authentication process for connection. Authentication of the remote system is done by the use of public-key cryptography and if necessary, it allows the remote computer to authenticate users.<br>
Both ssh and HTTP are protocols to communicate between client and server.<br>

The protocols can be broadly classified into three major categories: <br>
*Communication protocols* are really important for the functioning of a network. They are so crucial that it is not possible to have computer networks without them. These protocols formally set out the rules and formats through which data is transferred. These protocols handle syntax, semantics, error detection, synchronization, and authentication. (For example, HTTP, TCP, UDP, IP)<br>
*Management protocols* assist in describing the procedures and policies that are used in monitoring, maintaining, and managing the computer network. These protocols also help in communicating these requirements across the network to ensure stable communication. Network management protocols can also be used for troubleshooting connections between a host and a client. (For example, FTP, POP3)<br>
*Security protocols* secure the data in passage over a network. These protocols also determine how the network secures data from any unauthorized attempts to extract or review data. These protocols make sure that no unauthorized devices, users, services can access the network data. Primarily, these protocols depend on encryption to secure data. (For example, HTTPS, SSL)<br>

*Default ports for several data transfer protocols*<br>
HTTP - 80<br>
HTTPS - 443<br>
SSH - 22<br>
DNS - 53<br>
FTP - 20, 21<br>
POP3-110<br>

**Explain briefly: (1) what is IP, (2) what IPs are called 'white'/public, (3) and what happens when you enter 'google.com' into the web browser.**<br>
An *Internet Protocol* address (IP address) is a numerical label that is connected to a computer network that uses the Internet Protocol for communication. An IP address serves two main functions: network interface identification and location addressing.<br>

A *public IP* address is an IP address that is used to access the Internet. Public IP addresses can be routed on the Internet, unlike private addresses. 
The presence of a public IP address on router or computer will allow you to organize own server (VPN, FTP, WEB, etc.), remote access to computer, video surveillance cameras, and get access to them from anywhere on the global network.<br>
With a public IP address, we can set up any home server to publish it on the Internet: Web (HTTP), VPN (PPTP/IPSec/OpenVPN, WireGuard), media (audio/video), FTP, NAS, game server, etc.<br>

*What happens when you enter 'google.com' in the web browser*<br>
Resolve IP address of the URL via DNS<br>
Generate an HTTP request with headers (accept, user-agent, cookie, etc)<br>
Open an HTTP connection to the resolved IP address<br>
Send the request to the server<br>
Receive the response from the server<br>
Parse response headers<br>
Depending on the response headers, perform additional operations<br>
Decompress the response body if it's compressed<br>
Parse the HTML code inside the response body<br>
Resolve any additional resources (images, stylesheets, scripts, etc)<br>
Start loading those resources via their URLs using the same steps<br>
Render the HTML as soon as required resources are loaded, continue loading remaining resources in background<br>
When all the resources are loaded, close the HTTP connection<br>

**What is Nginx? How does it work on the high level? List several alternative web servers.**<br>
*NGINX* is open source software for web serving, reverse proxying, caching, load balancing, media streaming, and more. It started out as a web server designed for maximum performance and stability. In addition to its HTTP server capabilities, NGINX can also function as a proxy server for email (IMAP, POP3, and SMTP) and a reverse proxy and load balancer for HTTP, TCP, and UDP servers.<br>

*How does NGINX work*<br> 
Nginx is built to offer low memory usage and high concurrency. Rather than creating new processes for each web request, Nginx uses an asynchronous, event-driven approach where requests are handled in a single thread.<br>
With Nginx, one master process can control multiple worker processes. The master maintains the worker processes, while the workers do the actual processing. Because Nginx is asynchronous, each request can be executed by the worker concurrently without blocking other requests.<br>

NGINX uses a predictable process model that is tuned to the available hardware resources:<br>
The master process performs the privileged operations such as reading configuration and binding to ports, and then creates a small number of child processes (the next three types).<br>
The cache loader process runs at startup to load the disk‑based cache into memory, and then exits. It is scheduled conservatively, so its resource demands are low.<br>
The cache manager process runs periodically and prunes entries from the disk caches to keep them within the configured sizes.<br>
The worker processes do all of the work! They handle network connections, read and write content to disk, and communicate with upstream servers.<br>

*Several alternative NGINX*<br>
The best alternative is Apache HTTP Server, which is both free and Open Source. Other great apps like nginx are Caddy, lighttpd, Traefik and Varnish.<br>


**What is SSH, and for what is it typically used? Explain two ways to authenticate in an SSH server in detail.**<br>
The *SSH protocol* (Secure Shell) is a method for secure remote login from one computer to another. It provides several alternative options for strong authentication, and it protects the communications security and integrity with strong encryption.<br>

*Typical uses of the SSH protocol*<br>
The protocol is used in corporate networks for:<br>
-providing secure access for users and automated processes<br>
-interactive and automated file transfers<br>
-issuing remote commands<br>
-managing network infrastructure and other mission-critical system components.<br>

The two widely used *methods of SSH authentication* for secure remote access are:<br>
-Password authentication (using user name and passwords)<br>
-Public key-based authentication (using public and private key pairs)<br>
*Password-based authentication*<br>
In password-based authentication, after establishing secure connection with remote servers, SSH users usually pass on their usernames and passwords to remote servers for client authentication. These credentials are shared through the secure tunnel established by symmetric encryption. The server checks for these credentials in the database and, if found, authenticates the client and allows it to communicate. <br>
*Public key-based authentication*<br>
In Public key-based authentication, after the client establishes a connection with the remote server, the client informs the server of the key pair it would like to authenticate itself with. The server verifies the existence of this key pair in its database and then sends an encrypted message to the client. The client decrypts the message with it’s private key and generates a hash value which is sent back to the server for verification. The server generates its own hash value and compares it with the one sent from the client. When both the hash values match, the server is convinced of the client’s authenticity and allows it to communicate with the server.



## Problem

**Remote Server**
```bash
#Generate SSH key pair
ssh-keygen
```
```bash
cat .ssh/id_rsa.pub
```
```bash
#Connect to my server
ssh anastasiyavpunko@51.250.78.235
```
```bash
##Download the latest human genome assembly (GRCh38) from the Ensemble FTP server
wget https://ftp.ensembl.org/pub/release-108/fasta/homo_sapiens/dna/Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz \
wget https://ftp.ensembl.org/pub/release-108/gff3/homo_sapiens/Homo_sapiens.GRCh38.108.gff3.gz
```
```bash
#Install tools for our job
sudo apt-get update \
sudo apt-get install -y samtools \
sudo apt-get install -y tabix \
sudo apt-get install bedtools
```
```bash
#Index the fasta using samtools (samtools faidx) 
gzip -d Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz \ #unzip file
samtools faidx Homo_sapiens.GRCh38.dna.primary_assembly.fa   #get Homo_sapiens.GRCh38.dna.primary_assembly.fa.fai
```
```bash
#Index the GFF3 using tabix
gzip -d Homo_sapiens.GRCh38.108.gff3.gz \ #unzip file
(grep ^"#" Homo_sapiens.GRCh38.108.gff3; grep -v ^"#" Homo_sapiens.GRCh38.108.gff3 | sort -k1,1 -k4,4n) > Homo_sapiens.GRCh38.108.sorted.gff3 \ #sort
bgzip Homo_sapiens.GRCh38.108.sorted.gff3 \ #zip file
tabix Homo_sapiens.GRCh38.108.sorted.gff3.gz   #get Homo_sapiens.GRCh38.108.sorted.gff3.gz.tbi
```

Select and download BED files for three ChIP-seq and one ATAC-seq experiment from the ENCODE (cell line-K562)

```bash
#Download ChIP-seq
wget -O FOXA3.bed "https://www.encodeproject.org/files/ENCFF504WWL/@@download/ENCFF504WWL.bed.gz" \
wget -O MYC.bed "https://www.encodeproject.org/files/ENCFF664GSV/@@download/ENCFF664GSV.bed.gz" \ 
wget -O ZNF707.bed "https://www.encodeproject.org/files/ENCFF959ZKZ/@@download/ENCFF959ZKZ.bed.gz" \
# Download ATAC-seq
wget -O ATAC-seq-K562.bed "https://www.encodeproject.org/files/ENCFF855PCP/@@download/ENCFF855PCP.bed.gz"
```
```bash
#sort
bedtools sort -i FOXA3.bed > FOXA3.sorted.bed \
bedtools sort -i MYC.bed > MYC.sorted.bed \
bedtools sort -i ZNF707.bed > ZNF707.sorted.bed \
bedtools sort -i ATAC-seq-K562.bed > ATAC-seq-K562.sorted.bed 

#bgzip
bgzip FOXA3.sorted.bed \
bgzip MYC.sorted.bed \
bgzip ZNF707.sorted.bed \
bgzip ATAC-seq-K562.sorted.bed \

#index using tabix
tabix FOXA3.sorted.bed.gz \
tabix MYC.sorted.bed.gz \
tabix ZNF707.sorted.bed.gz \
tabix ATAC-seq-K562.sorted.bed.gz
```

**JBrowse 2**

```bash
#Download and install JBrowse 2. 
sudo apt-get install npm \
sudo npm install -g @jbrowse/cli \

#Create a new jbrowse repository.
sudo jbrowse create /var/www/html/jbrowse/
```

```bash
# Install nginx and amend its config
sudo apt-get install nginx
sudo nano /etc/nginx/nginx.conf
```
```
I added this:
server {
      listen 80;
      index index.html;   
  }
```  
  
```bash
#Restart the nginx (reload its config)
sudo /etc/init.d/nginx reload
```
Access the browser using a link: <br>
http://51.250.78.235/jbrowse/ 

```bash
jbrowse add-assembly Homo_sapiens.GRCh38.dna.primary_assembly.fa --load copy --out /var/www/html/jbrowse/
jbrowse add-assembly Homo_sapiens.GRCh38.dna.primary_assembly.fa.fai --load copy --out /var/www/html/jbrowse/

jbrowse add-track Homo_sapiens.GRCh38.108.sorted.gff.gz --load copy --out /var/www/html/jbrowse
jbrowse add-track Homo_sapiens.GRCh38.108.sorted.gff3.gz.tbi --load copy --out /var/www/html/jbrowse

jbrowse add-track FOXA3.sorted.bed.gz --load copy --out /var/www/html/jbrowse
jbrowse add-track FOXA3.sorted.bed.gz.tbi --load copy --out /var/www/html/jbrowse
```

## Extra points

**OSI модель**<br>
Это модель, с помощью которой общаются различные устройства. Например, так компьютер взаимодействует с роутером.<br>
Она состоит из семи уровней и у каждого уровня своя функция в этом взаимодействии. <br>
Перед тем как перейти к рассмотрению уровней введем понятие PDU (Protocol Data Unit) - это обобщенное понятие того, что несет в себе каждый уровень.<br>

*1)Физический.*<br> Здесь происходит передача информации, путем отправления сигнала от отправителя к получателю. Железо в компьютере понимает эту информацию только в виде набора нулей и единиц, то есть бит. Они передаются по кабелям или без — например, через Bluetooth или Wi-Fi.<br>
PDU - бит.<br>
*2)Канальный.*<br> Этот уровень получает биты и превращает их в кадры с адресом отправителя и получателя, после чего отправляет их по сети. Адресом является MAC адрес. Сформированные кадры от одного устройства к другому передают коммутаторы. Здесь выделяют два подуровня: MAC (отвечает за присвоение физических MAC-адресов) и LLC(занимается проверкой и исправлением данных, управляет их передачей).<br>
PDU - кадр. <br>
*3)Сетевой.*<br>
На этом уровне MAC-адрес от коммутаторов с предыдущего уровня переходит на маршрутизаторы, которые строят  маршрут от одного устройства к другому с учетом всех потенциальных неполадок в сети. Адресация здесь происходит по IP-адресам. 
Например, пользователь желает перейти на сайт и вводит его адрес, отправляется DNS-запрос. Ответом на него будет IP-адрес, который подставляется в пакет. <br>
PDU - пакет.<br>
*4)Транспортный.*<br>
На этом уровне происходит транспортировка пакетов. При транспортировке возможны потери и задержки, поэтому для разных данных используются разные протоколы. Например, если в тексте потеряется часть слов, то будет сложно понять смысл, поэтому при передаче данных, чувствительных к потерям, используется протокол TCP, контролирующий целостность доставленной информации.
А для видеофайлов небольшие потери не так важны, критичнее будет задержка. Для передачи данных, чувствительных к задержкам, используется протокол UDP, позволяющий организовать связь без установки соединения.
При передаче по протоколу TCP данные делятся на сегменты (чтобы увеличить пропускную способность или чтобы избежать потери большого пакета). При передаче данных по протоколу UDP пакеты данных делятся уже на датаграммы.<br>
PDU сегмент/датаграмма.<br>
*5)Сеансовый.*<br>
Этот уровень ответственен за организацию сеансов связи, обмен информацией.
Например, мы созваниваемя по видеозвонку, в это время необходимо, чтобы два потока данных (аудио и видео) шли синхронно. Когда к разговору двоих человек прибавится третий — получится уже конференция. Задача пятого уровня — сделать так, чтобы собеседники могли понять, кто сейчас говорит.<br>
PDU - данные.<br>
*6)Представительский.*<br>
Этот уровень осуществляет преобразование форматов данных, например, сжатие и кодирование. Здесь происходит представление картинок и видео-аудио данных. А помимо этого, шифрованием данных, если при передаче их необходимо защитить.<br>
PDU - данные.<br>
*7)Прикладной.*<br>
Прикладной уровень — это то, с чем взаимодействуют пользователи, своего рода графический интерфейс всей модели OSI. Задача этого уровня состоит в том, чтобы пользователь увидел данные в понятном ему виде.
Сюда относятся протоколы для просмотра страниц в интернете (HTTPS, HTTP), для работы с почтовыми службами (SMTP, POP3), для передачи файлов (FTP, TFTP) и другие.<br>
PDU - данные.<br>

**TCP/IP**<br>
TCP/IP также является сетевой моделью, но в ней только 4 уровня. Здесь также как и в OSI внутри каждого уровня действуют определенные протоколы и выполняются собственные функции.<br>

*1)Канальный.*<br>
Этот уровень описывает то, как происходит обмен пакетами данных через физический уровень и как именно информация передается от одной машины к другой.
Информация здесь кодируется, делится на пакеты и отправляется по нужному каналу.<br>
PDU - бит/кадр.<br>
*2)Сетевой.*<br>
Этот уровень занимается соединением существующих локальных сетей в глобальную.
И сетевой уровень также отвечает за адресацию хостов, упаковку и функции маршрутизации. 
Именно этот уровень является одним из ключевых принципов функционирования Интернета. Локальные сети объединяются в глобальную, а благодаря пограничным и магистральным маршрутизаторам между ними осуществляется передача файлов.
Основной протокол - IP (отвечает за IP-адресацию, маршрутизацию, фрагментацию и повторную сборку пакетов).<br>
PDU - пакет.<br>
*2)Транспортный.*<br>
Основными протоколы этого уровня - TCP и UDP.
TCP — надежный, обеспечивает передачу информации, проверяя дошла ли она, насколько полным является объем полученной информации и т.д. 
UDP — ненадежный, он занимается передачей автономных датаграмм. UDP не гарантирует, что всех датаграммы дойдут до получателя. <br>
PDU - сегмент/датаграмма.<br>
*3)Прикладной.*<br>
На этом уровне работает большинство сетевых приложений. Эти программы имеют свои собственные протоколы обмена информацией, например, HTTP для WWW, FTP (передача файлов), SSH (безопасное соединение с удалённой машиной) и т.д.<br>
PDU - данные.
