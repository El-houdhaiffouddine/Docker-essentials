# Docker-essentials
This project initiate you with the basics you need to know about Docker.
Let's define what's Docker before entering in depth in the project.
<h1>What is Docker ?</h1><br/>
<b>Docker</b> is a platform that allow Developers to create, run, test and deliver fastly an application.<br>
<h2>How Docker works ?</h2><br/>
<b>Docker</b> works by using the client-server architecture. The client is your terminal which allows you to write your docker commands (<b>docker run, docker build, docker stop, ...</b>) to interact with the server which is the <b>Docker daemon (dockerd)</b>. The client and the server communicate via REST API or UNIX socket or network interface.<br/>
<h2>Docker keywords</h2><br/>
<ul>
<li>Docker image</li>A <b>Docker image</b> is a read-only specific file that permits to create a container. To generate this image, we write some instructions in a file called Dockerfile (will be studied in a future section) which the docker daemon uses to generate the image.<br/>
<li>Docker container</li> <p>A <b>Docker container</b> is a runnable instance of an image which is isolated from other containers and the host system which runs Docker.</p><br/>
<li>Docker daemon</li> A <b>Docker daemon</b> is the heart of Docker which manages and treats all the requests sent by the <b>Docker client</b>. The daemon is the responsible on how Docker works.<br/>
<li>Docker registry</li> A <b>Docker registry</b> is a specific place in which docker images are stored. An example of a Docker registry is <b>Docker Hub.</b> Docker Hub is a public Docker registry which allows each one to access, pull and push Docker images.

</ul>
<h2>Docker networking</h2><br/>
<p>Imagine you have a web server and a database both running in a containers and you wanna send some SQL(Structured Query Language) requests to retrieve data from the database. Without networking, the container web server can't communicate with the container database to retrieve those data. Networking allows 2 or more containers to communicate together. By default, when a docker container is created without being assigned to a network driver, this one inherits the <b>bridge driver</b> which automatically created when docker is installed in the host operating system. That means all containers created without being assigned to a network driver, can communicate between each other.<br/>
In Docker, there's 3 ways to create a network by using one of the following network driver:<br/>
<ul>
<li><b>Bridge driver:</b> This drive allows to create a network which is isolated from other containers which are not connected to the same drive network. The advantage of this drive, it permits you to interconnect more docker containers located in the same docker daemon host.</li>
<li><b>Host driver:</b>This driver create (copy) all the network interfaces of the host operating system in which Docker has been installed in the container to create the container network. It means that the container network is not isolated from the host network. The benefit of this network driver is that you can create more services and make them communicate by ports (UDP or TCP ports connections).</li>
<li><b>Overly driver:</b> This driver is very useful if you want to connect different containers located in different Docker daemons. The goal of this driver is to connect multiple Docker daemons together rather than using OS-level routing.</li>
<li><b>IPvlan driver:</b>This network allows you to create a virtual LAN network to connect containers together. With VLAN, you can create more sub-interfaces by using a single interface (For example, eth0) to interconnect more devices (Containers) in the network.</li>
<li><b>MACvlan driver:</b>This driver allows you to create docker networks and make containers communications with MAC (Media Access Control) addresses. When container-1 wants to cmmunicate with container-2, rather than using an IPv4 address, they will both use MAC address to communicate together. When this driver is assigned to a container, the Docker daemon routes traffic to it destination via MAC address.</li>
<li><b>None:</b> This option allows you to completely isolate the container from the host operating system and other containers. </li>
</ul>
<h2>Docker storages</h2><br/>
When a container is stopped or restarted, all its data are deleted. To avoid this problem, Docker comes with <b>Docker volumes</b>. A Docker storage is a way to persist your data from the container. This is very important in some cases like when you run a mysql database inside a container.<br/>
Docker has created 4 ways to persist your data when you are running a container which are:<br/>
<ul>
<li><b>Volumes mounts:</b> A volume is the best way to persist container data in Docker. When this volume type is specified, Docker creates a file system in the host operating system which is mounted by the Docker daemon when you run your container. All the container data are persisted (stored) in that file system in the host operating system. Direct access to the host file system in the container is unsupported by this storage type and even when you delete completely your docker container, all stored data in the volume doesn't diseaper.</li>
<li><b>Bind mounts:</b> This type of storage allows the container to have a direct access to the host file system which can causes security issues. The philosophy of this storage is the same as the one from the volume but their differences reside in the accessibility of the host file system.</li>
<li><b>tmpfs mounts:</b> This type of storage allows you to store or persist container data in the memory (RAM) rather than saving them in the hard disk of the host operating system. You can use this storage if you are managing ephemere data. 
</li>
<li><b>Named pipes:</b> A named pipe (FIFO: first in, first out) in the programming language, is a way to create specific files and allow processes to read and write inside that files and communicate together. In Docker, named pipe are used to create a communication between a container (a program in a container) and the Docker API.   </li>
</ul>
<h2>Docker compose</h2><br/>
<b>Docker compose</b> is a tool which allows you to build and run multiple containers as services in a single YAML file. 
For example, if you wanna interconnect your frontend and backend web app within Docker, you have to use Docker compose by specifying all your needs (networks, images, volumes, configs, ...) in the YAML file and run a single command to launch them one time.
 Docker compose made easy the manipulation of Docker technology.<br/>
<h2>How to create a Docker image and run a Docker container ?</h2><br/>
In this section, we are going to see how to create a docker image and how to transform that image into a container.
Creating a docker image and transform it into a docker container requires 3 steps which are : Writing the Dockerfile content, building the docker image and creation of the docker container.<br/>
<h3>1. Writing the Dockerfile content</h3><br/>
A Dockerfile is a specific text file without extension (example, .exe, .txt, pdf) used in Docker to write all the necessary instructions that the Docker engine should use to build (create) a docker image.
Creating a docker image, requires the creating of this file by naming it <b>Dockerfile</b> or with your preferred name. Once you created this file, you can add your preferred instructions inside the file and then build your docker image.
A docker instruction is just a simple docker command followed by options which are used by the docker daemon to create the docker image. A docker instruction is composed by a code mneumonic plus options and its input (example: os commands, ... ):<b> docker-instruction [option1 option2 ...] input</b>.<br/>
An example of a docker instruction is:<b>VOLUME /home/user1/storage1 /tmp/storage1 </b> which sets a volume to persist container data.<br/>
Each docker instruction create a new layer on top of the current image. A docker is updated only if you edit its corresponding instruction or you specify <b>-- no-cache</b> during the building stage of the docker image.<br/>
<h4>Common docker instructions:</h4><br/>
<ul>
<li><b>FROM:</b> This is the foundation of your docker image and it specifies the base image of your docker image that subsequent instructions will build upon. Most of Dockerfile should contain this instruction.</li>
<li><b>RUN:</b> Runs os commands to install packages and build applications and configure the environnement.</li>
<li><b>ADD:</b> Allows you to copy both local and remote files and directories (git files, zip files, ...) into your docker image.</li>
<li><b>COPY:</b> Copies local files and directories from your host operating system to your docker image. </li>
<li><b>ENV:</b> Creates environnement variables that will be used with other docker instructions to create the docker image.</li>
<li><b>WORKDIR:</b> Sets the working directory for subsequent instructions that follow it in the Dockerfile (ENTRYPOINT, RUN, CMD, ...).</li>
<li><b>USER:</b> Defines or sets the user that the docker engine will use to run subsequent commands. This user will be the default user of the running container.</li>
<li><b>VOLUME:</b> It used by the docker engine to create a specific volume (storage) to persist data from the container. This is very useful if you wanna persist data from a database container or you have critical data that need to be saved.</li>
<li><b>ENTRYPOINT:</b> It used to specify the default command which will be run in the container</li>
</ul>
<p>To write our Dockerfile content, we are going to use a simple Flask application which manages Employees by doing CRUD(Create Read Update Delete). Feel free to access on the source code of the App by clicking <a href="https://github.com/El-houdhaiffouddine/Python_with_Flask.git">here</a>. So the principal goal of the docker image we are going to create is about to run that Flask App in a docker container. We named our Dockerfile with the name <b>Flask-App</b>. Feel free to read it <a href=#>here</a>.<br/></p>
<h3>2. Building the docker image</h3><br/>
 <p>Once we finish to write our Dockerfile content, the next step now is to build our Docker image. Building a Docker image means running the <b>docker build</b> command. In our case we should run that command as follows: <b>docker build -t flask-app:1.0.0 -f Flask-App .</b> that command will create a docker image which contains the Flask App. <b>-t</b> specifies the tags of our docker image.<b>-f</b> specifies the name of our Dockerfile image which is Flask-App. By default, the Dockerfile is named<b>Dockerfile</b> and if it has this specific name so you don't need to specify the option <b>-f</b>. <b>.</b> specifies the exact location of the Dockerfile which in this case is located in the same directory we runs the docker command.<br/></p>
 <h3>3. Creation of the docker container</h3><br/>
<p>Creating a docker container means run the following command: <b>docker container create --name flask-container flask-app:1.0.0</b>. <b>--name</b>allows us to specify the container name. Once the container is created, we can run it and the start interacting with the Flask App. To do that, we have to run the following command:<b>docker container run flask-container</b>. That command will start the flask container and automatically the Flask App will be accessible on 8080 port.</p>
</p>


