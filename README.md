# Docker-essentials
This project initiate you with the basics you need to know about Docker.
Let's define what's Docker before entering in depth in the project.
<h1>What is Docker ?</h1><br/>
<b>Docker</b> is a platform that allow Developers to create, run, test and deliver fastly an application.<br>
<h2>How Docker works ?</h2><br/>
<b>Docker</b> works by using the client-server architecture. The client is your terminal which allows you to write your docker commands (<b>docker run, docker build, docker stop, ...</b>) to interact with the server which is the <b>Docker daemon (dockerd)</b>. The client and the server communicate via REST API or UNIX socket or network interface.<br/>
<h2>Docker keywords</h2><br/>
<ul>
<li>Docker image</li> A <b>Docker image</b> is a read-only specific file that permits to create a container. To generate this image, we write some instructions in a file called Dockerfile (will be studied in a future section) which the docker daemon uses to generate the image.<br/>
<li>Docker container</li> A <b>Docker container</b> is a runnable instance of an image which is isolated from other containers and the host system which runs Docker.<br/>
<li>Docker daemon</li> A <b>Docker daemon</b> is the heart of Docker which manages and treats all the requests sent by the <b>Docker client</b>. The daemon is the responsible on how Docker works.<br/>
<li>Docker registry</li> A <b>Docker registry</b> is a specific place in which docker images are stored. An example of a Docker registry is <b>Docker Hub.</b> Docker Hub is a public Docker registry which allows each one to access, pull and push Docker images.

</ul>
<h2>Docker networking</h2><br/>



