#  Docker 
Docker is an open platform for developing, shipping, and running applications.
## > What is docker?
* Docker (dock worker) is used to create containers which is standard way of packaging any application.


![preview](./Images/docker1.png)

### > Docker Architecture
* Earlier docker architecture had only two components

![preview](./Images/docker2.webp)

* Then docker has made the changes in architecture with layered components.

![preview](./Images/docker3.webp)

* #### docker client: 
docker client/command line to interact with daemon
* #### docker daemon: 
This is service which forwards the request to containerd 
* #### containerd: 
manages the container lifecycle
* #### runc:
 This creates container using libcontainer
* #### shim: 
once the contianer is created runc makes shim the parent of container, this helps docker containers to be in running state even if the docker components are upgrading.
## > Docker installation :
1. Create a linux vm (ubuntu 22.04)
2. use the docker installation script  (Docker script)
   * $ curl -fsSL https://get.docker.com -o install-docker.sh
   * $ sh install-docker.sh 
   * $ docker version

![preview](./Images/docker4.PNG)   ![preview](./Images/docker5.PNG)
   * you will see the failure to get the server version
   * The reason is the user doesnot have permission to access unix socket at unix:///var/run/docker.sock. The permission to this exists for all the members of docker group, so lets add the current user to docker group.
3. * $ sudo usermod -aG docker <user-name>
   * $ exit  #(relogin)
4. open all ports (inbound rules in azure, n/w security grp in aws)

![preview](./Images/docker6.PNG)   ![preview](./Images/docker7.PNG)

### > Dcoker container way of working
![preview](./Images/docker8.PNG)
### > What happens
* docker client will forward the request to docker daemon
* docker daemon will check if the image exists locally. if yes creates the container by using image
* if the image doesnot exist, then docker daemon tries to download the image from docker registry connected. The default docker registry is docker hub.
* Downloading image into local repo from registy is called as pull.
* Once the image is pulled the container is created.

### > lets pull the nginx image 
  * $ docker run nginx        (latest version)
  * $ docker run nginx:1.22   (name:x.xx - version)

![preview](./Images/docker10.PNG)

* list of images
  * $ docker image ls 

![preview](./Images/docker11.PNG)  

* deleting selected image and deleting all images at a time
  * $ docker image rm nginx
  * docker image rm $(docker image ls -q)

![preview](./Images/docker12.PNG)

### > docker container lifecycle
* Created
* Running
* Paused
* Stopped
* Deleted

![preview](./Images/docker9.PNG)

### > Create a container with nginx
* to start and run the container use 'run' command
  * $  docker container run -d --name nginx1 nginx

![preview](./Images/docker13.PNG)

* to check list of running containers  
  * $  docker container ls
*  to check list of all containers(irrespective of state)  
  * $  docker container ls -a

![preview](./Images/docker14.PNG)

* to stop the container  
  * $  docker container stop nginx12

![preview](./Images/docker15.PNG)

* pause and unpause the container
  * $ docker container pause nginx123
  * $ docker container unpause nginx123

![preview](./Images/docker16.PNG)

* delete the paticular container
  * $ docker container rm -f nginx123

![preview](./Images/docker17.PNG)

*  delete all containers
  * $ docker container rm $(docker container ls -a -q)

![preview](./Images/dpcker18.PNG)

### > port-forwording
 * p - we need to give the port 
   * $  docker container run -d -p 30000:80 --name nginx1 nginx
 * P - it automatically takes the port number
   * $  docker container run -d -P --name nginx1 nginx

![preview](./Images/docker19.PNG)
![preview](./Images/docker20.PNG)
![preview](./Images/docker21.PNG)













 























 
   
   

