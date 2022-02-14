# Dockerrefresher


# why use docker


![image](https://user-images.githubusercontent.com/80065996/152994730-c378f241-0acf-46b2-ba65-dc72c2e6b3cd.png)


# Task to implement the redis - the traditional problematic way 


**Go to the site: https://redis.io/download**

**Follow the steps in installation page by copying it and pasting it manually one by one in command line


![image](https://user-images.githubusercontent.com/80065996/152996223-74dfd36c-e3fb-4542-8577-215b543b64b8.png)


# Instead of doing this in traditional way we can do it via docker by using single command
# with single docker run command we have achieved the same redis installation as shown below and database will be ready to accept connections


![image](https://user-images.githubusercontent.com/80065996/152996688-c1a82e44-5f46-46b6-bcb7-b7f3b75c6aeb.png)



![image](https://user-images.githubusercontent.com/80065996/152997365-2d274356-4816-430b-b6d1-c04c7137a613.png)


# Docker ecosystem:


![image](https://user-images.githubusercontent.com/80065996/152997733-299d05a4-2336-4ef6-9468-96a0a93214c7.png)


# image to container Relationship


![image](https://user-images.githubusercontent.com/80065996/152998132-d5038f58-e165-4665-bd59-44e4b57d332d.png)


# container is the instance of the image and we can create any number of containers from the single image


# command to check whether docker is installed


![image](https://user-images.githubusercontent.com/80065996/152998741-021a0324-f6ea-4835-8a41-37ca3eb48a53.png)


# What is happening when we give 'Docker run' command


![image](https://user-images.githubusercontent.com/80065996/152999134-7f5770c3-6264-48e7-8636-88708390f15e.png)


![image](https://user-images.githubusercontent.com/80065996/152999596-c0524dfb-77fb-4ca0-8521-54524130a173.png)


# 1) the command you have typed will be passed to 'docker client' which then called 'docker daemon(server)'. 'Docker Daemon' will call the 'Docker hub' 
# for the image we are looking for. Once the image is found, it will download from docker hub and keep it in 'image cache'. The next time if we request the same image 
# to create a container. docker dameon will be clever enough to identify the image in 'image cahce' locally and then take it instead of going to docker hub for every request
# This is another reason why docker is very fast


# first time - Docker getting 'hello-world' image from Docker hub. it will give message 'unable to find locally'


![image](https://user-images.githubusercontent.com/80065996/153000668-746f6999-22f4-4da7-a2ff-d739217f833e.png)


# second time - no message that 'unable to find locally' because docker found this file in local 'image-cache' rather than looking in docker hub


![image](https://user-images.githubusercontent.com/80065996/153000782-7a8c146d-d22f-4dbc-b2ac-9ac40cfe6bde.png)


# What is container - how our system works


![image](https://user-images.githubusercontent.com/80065996/153001441-6da2c919-c74a-43f6-84f0-9b6a47c5c32c.png)


# To Understand how docker works we need to know how Kernel works. When we get a laptop first thing we do is intalling operating system
# Operating system will get instruction from user and perform the operation in computer hardware.
# so operating system is intermediate layer between user and computer
# once you install the operating system, we need to install various apps like chrome, spotify and many other softwares. These softwares will store the data and retireve
# the data from computer hardware by using "system calls" to Kernel. Kernel from the operating system will call the underlying hardwares like CPU, memory for any operations


# critical sceario:


![image](https://user-images.githubusercontent.com/80065996/153006833-a9476c18-8423-4515-8e13-55e3ab5d4efb.png)


# We have only python-2 installed in our computer hard disk. 
# Now we want to install 2 softwares. Google chrome which requires 'python 2' as a dependency and 'node js' which requires 'python-3' as a dependency in the computer
# at a single given point of time we can install only 'python-2' or 'python-3' and not both
# So how are we going to install both these softwared ? -  This is the scenario where exactly docker comes into the picuture


# solution to this issue: --  Container stores all the data and dependencies in the namespace (parition in the hard disk of server)
# We can create segment parition in the hard disk and in one of the segment we can install python-2 and other segment we can install python-3


![image](https://user-images.githubusercontent.com/80065996/153008042-0ee38d9b-388d-42ef-a0a6-518edd28269c.png)


![image](https://user-images.githubusercontent.com/80065996/153008229-8167bfc2-9608-4cbf-8c6a-90fcc87972d8.png)


![image](https://user-images.githubusercontent.com/80065996/153010152-9db0d0e4-2812-42f6-ba4c-8c3b88835503.png)


# so as per above solution if chrome calls for any operation, the kernel will redirect the call to harddisk segment having python-2
# and if 'Nodejs' calls for any operations kernel will redirect the call to hard disk parition having python-3


# Here comes the concept of 'Namespaces' and 'Control groups'. --  Container stores all the data and dependencies in the namespace (parition in the hard disk of server)


![image](https://user-images.githubusercontent.com/80065996/153011151-ccf6bc0d-5c73-4310-8350-d454f39e1e06.png)


# 'Namespace' := it will control the number of process(like chrome and other software used paython 2 ) that hard disk going to use. every harddisk parition created namespaces.
# 'Control group' :=  it will control CPU and memory usage by process using that particular namespace so that many process can run without any deadlock


# Structure of container : --  Container stores all the data and dependencies in the namespace (parition in the hard disk of server)

# PORTION OF HARD-DISK ALONG WITH SOME PORTION OF KERNEL ALONG WITH THE SOFTWARE PROGRAM RUNNING CALLED CONTAINER.BELOW DIAGRAMS EXPLAINS CLEARLY


![image](https://user-images.githubusercontent.com/80065996/153011747-2b6139f0-5a5d-4735-8fda-4d23962e9769.png)


![image](https://user-images.githubusercontent.com/80065996/153011782-7689b449-4e05-4a1a-96c3-04facce6eb7d.png)


# HOW IMAGE WILL BE RELATED TO CONTAINERS GETTING CREATED


![image](https://user-images.githubusercontent.com/80065996/153027809-2c1842b2-d58a-4db2-81fe-a5a9ed1d9b35.png)


# Image contains 2 parts 
# 1) File system snapshot (Operating system files + chrome + Python2)  
# 2) Start up command to start chrome 


# Image architecture


![image](https://user-images.githubusercontent.com/80065996/153029497-9f413785-4076-4acb-9d85-b5847515cc3a.png)


# So if we run the image, it will create a container with (operating system file system snapshot with python and chrome installed in namespace of Server's hard disk) 
# Container will be created using startup command from the image
# Containers are isolated environments in the namespace so one container cannot access the contents inside other container 


# Below image shows how container's (file system snapshot (os file+python+chrome) is getting stored in namespace (parition created in hard disk of sever))


![image](https://user-images.githubusercontent.com/80065996/153030749-fbcdf65d-1904-4749-8da6-265f8d703de5.png)


# startup command invoked the chrome.exe file namespace of the hard disk of the server. so that chrome will start running inside the container


![image](https://user-images.githubusercontent.com/80065996/153031456-b737f3e9-706d-4ebb-99cd-a99139429bac.png)


# NAMESPACE AND CONTROL GROUPS ARE SPECIFIC TO LINUX OPERATING SYSTEM. THEN HOW DOCKER WORKING ON OTHER OPERATING SYSTEM ?
# ANSWER: LINUX VIRTUAL MACHINE WILL BE STARTED ON TOP OF OPERATING SYSTEM WE HAVE IN OUR COMPUTER SO THAT CONTAINERS WILL RUN INSIDE THE VIRTUAL MACHINE


# HERE IS HOW DOCKER WORKS:

# DOCKER FILE WILL MENTION THE OPERATING SYSTEM (FROM GOLANG:ALPINE:3.8.2). OPERATING SYSTEM WITH GOLANG INSTALLED. ALPINE IS COMPRESSED VERSION OF LINUX OS
# WE CAN MENTION 'COPY' COMMAND TO COPY THE FILES TO THE FOLDERS IN OPERATING SYSTEM
# USE 'RUN' CMMAND TO INSTALL ANY PACKAGE INSIDE THE FILE SYSTEM SNAPSHOT
# ONCE FILE SYSTEM SNAPSHOT WITH ALL THE DEPENDENCIES ARE READY MENTION THE STARTUP COMMAND AT THE LAST USINF 'CMD'.
# BUILD THIS DOCKER FILE AND CREATE THE IMAGE AND PUSH TO DOCKER HUB
# DOCKER RUN COMMAND WILL PICK THIS IMAGE FROM DOCKER HUB. FROM THE IMAHE FILE SYSTEM SNAPSHOT WILL BE PUT INSIDE THE NAMESPACE OF SERVER'S HARDDISK WE RAN DOCKER RUN COMMAND
# ALSO CONTAINER BODY CREATED BY TAKING PART OF HARD DISK, PART OF KERNEL. 
# NEXT STARUP COMMAND WILL INVKE THE EXE FILE CREATED AS PART OF BUILD WHICH IS PRESENT IN FILE SYSTEM SNAPSHOT INSIDE THE CONTAINER BODY


# Demystifying ' docker run ' command


![image](https://user-images.githubusercontent.com/80065996/153038254-9059a2ff-d410-40e9-bee2-cb81c85d6a50.png)


# Docker run hello-world -- how its working - below image explains that


![image](https://user-images.githubusercontent.com/80065996/153038629-e835b6b8-7769-4200-a8e4-aa60085c5c9e.png)


# Overriding default startup command


![image](https://user-images.githubusercontent.com/80065996/153145450-7dbd2363-72bf-4ea2-9df0-15871d772fcf.png)


![image](https://user-images.githubusercontent.com/80065996/153146835-fd9a0b35-1349-46e5-8cd4-b144595ad9fe.png)


# we have created container from busybox image and overridded default command. busybox file system will be of linux file system so echo command works perfectly


# first time it pulled from docker hub. now running for the second time


![image](https://user-images.githubusercontent.com/80065996/153147810-8ee1062e-3997-4021-80a8-8b9740d41a39.png)


# by overriding default start up command, below is the example of seeing linux file system of the container created from busybox image in the namespace(hard disk) of EC2 server i am running.


![image](https://user-images.githubusercontent.com/80065996/153149467-365820f9-3732-4eb5-b298-19cb6c0c809c.png)


# busybox archotecure


![image](https://user-images.githubusercontent.com/80065996/153150039-cdd7ffbc-c39e-41b1-a8f6-ed09af43489e.png)


# after giving docker run command


![image](https://user-images.githubusercontent.com/80065996/153150329-f05cd271-cc9a-4970-a5c5-8df5789cb8db.png)



# how command 'ls' and 'echo' works in busybox image. Why beacuse somewhere inside the folders of the linux file system snapshot we have the executables so once we give the 
# name of the executables it runs perfectly. The same thing if you try in 'hello-world' image it wont work because 'hello-world' image does not have any filesystem snapshot
# 'hello-world' image just a basic image to display some text


# Listing all the only running containers


![image](https://user-images.githubusercontent.com/80065996/153152873-6e7f1c7d-0ac2-48e5-891e-d63a6249d77c.png)


![image](https://user-images.githubusercontent.com/80065996/153152979-ee0e5edc-f0b3-425e-a3e1-73a795a4ac04.png)


# In order to see running containers using 'docker ps' command container should be in running state. if a container starts and exits immediately we cannot see that 
# container using 'docker ps' command


![image](https://user-images.githubusercontent.com/80065996/153154197-ceb747db-f4f4-4b28-8594-a594f04f5862.png)


# above image you could see busybox container started and exited immediately so we could not able to see the container using 'Docker ps' command.
# so Container needs to be in running state for sometime.

# We can use 'Docker ps -a' command to see all containers in any of its lifecycle


# just experimenting with the container and making container to run for sometime.

# Make the default command of the busybox image as 'ping www.google.com' so that container will keep on pinging google so that we can keep the container in running state


![image](https://user-images.githubusercontent.com/80065996/153155054-3b437dcd-2832-40f7-b334-74afdb2d414b.png)


# now open another git bash terminal and issue the command 'docker ps' so that we can see container in running state


![image](https://user-images.githubusercontent.com/80065996/153155099-4c6ac143-f77c-4f69-9054-8eaf60f15af7.png)


# command to check containers in any state


![image](https://user-images.githubusercontent.com/80065996/153156192-451aa5a9-9ae7-4836-bab7-83906f0646dd.png)


# 'Docker run == Docker create + Docker start'


![image](https://user-images.githubusercontent.com/80065996/153192689-88ac516c-545f-48f8-8180-597aa10767c0.png)



![image](https://user-images.githubusercontent.com/80065996/153192815-0dd42dc9-e467-4156-a38f-3658b3953c9e.png)



# Difference between creating a container and starting a container

# Creating container - copy the file system snapshot with all the dependecnies from docker image to the hard disk's namespace of the server.


![image](https://user-images.githubusercontent.com/80065996/153193172-dc83c014-d5b9-4f77-91d4-237e636adbf9.png)


# starting a container - executing the startup command


![image](https://user-images.githubusercontent.com/80065996/153193322-cb98af59-8ee2-458a-9097-e3b117eab6fa.png)


# 'Docker create' command


![image](https://user-images.githubusercontent.com/80065996/153224485-b30f240d-9dd5-4a11-80a4-e775437ced8b.png)


# 'Docker create' command will pull the image and copy the file system snapshot to namespace of server hard disk. 
# we will get hash id. we can copy the hash id and then with the hash id you can issue the command 'docker run hasid'. This starts the container


![image](https://user-images.githubusercontent.com/80065996/153225074-8ddd0bd5-f493-472e-aa7e-ddc975258faf.png)


# While giving 'docker run' command use flag (-a) to see the logs.


# Restarting a stopped container. if a container is stopped it does not mean that the container is dead. we can restart the container at any point of time


# below are two container which are in 'Exited' state.


![image](https://user-images.githubusercontent.com/80065996/153227563-86efb365-7168-4a9a-876a-3cc00a5d08bf.png)


# used 'Docker start -a container_id' command to restart the stopped container


![image](https://user-images.githubusercontent.com/80065996/153227701-ffd32afa-0003-44d3-b8f1-487058cbe9bd.png)



![image](https://user-images.githubusercontent.com/80065996/153228492-9e2e623b-846a-4280-a5ec-0b67766902e7.png)


# Whenever you restart the stopped container, it will execute the overrided start up command if any everytime. if no overrided command, default command 
# will be executed by default


# 'docker system prune' - it removes 1) all stopped containers 2) all dangling images 3) unused network 4) all build cache as listed below 


![image](https://user-images.githubusercontent.com/80065996/153237455-881e983d-39b2-470b-8897-418e63f1e97d.png)


![image](https://user-images.githubusercontent.com/80065996/153237769-649dd586-323d-476f-bb88-88b91e4be5ac.png)


# getting logs from container


![image](https://user-images.githubusercontent.com/80065996/153244447-95b4cf78-2fce-4810-b1f3-2bf771d2bd0d.png)


![image](https://user-images.githubusercontent.com/80065996/153245356-f9a715bb-f23b-4fb5-b946-78a84d169aa0.png)


# killing or Stopping docker container


![image](https://user-images.githubusercontent.com/80065996/153246289-1d0b352b-64ad-4b02-8373-7e7f97f7bb9f.png)


# Stopping a docker container


![image](https://user-images.githubusercontent.com/80065996/153246593-45c2009b-f745-4c17-b7e0-fbdf956393fa.png)


# Killing a docker container


![image](https://user-images.githubusercontent.com/80065996/153247299-db51fbcc-8f09-4840-a304-fb85007e2545.png)


# "Docker stop" will take few time to terminate a container. it is called graceful shutdown. Since docker is written in golang we can implement this
# "Docker kill" wont take any time. it will kill the continer very quickly


# Example := How to install and use Redis using Docker 


![image](https://user-images.githubusercontent.com/80065996/153249055-2d800b60-025e-4e4b-ba26-43d8ffa256e4.png)


# Going to install both 'Redis-server' and 'Redis-client'


# step 1: created a redis container


![image](https://user-images.githubusercontent.com/80065996/153250258-0459c780-2ec3-4500-bd93-c95bd3fbdf2e.png)


# step 2: open another git bash terminal and install redis client and try to access redis-server running inside the container we just created for redis-server
# you can see i have installed 'redis-cli' in the system instead of creating a container and installing inside of it


![image](https://user-images.githubusercontent.com/80065996/153250796-8a50efd8-e7ba-4fda-a47c-c398c0e724b6.png)


# But the moment you have given "redis-cli" and try to connect to "redis-server" running inside the another container, it will throw error "connection refused"


![image](https://user-images.githubusercontent.com/80065996/153252222-d550789b-5a41-43a2-b5cf-3ed51498eef4.png)


# Reason why we got "connection refused" error


![image](https://user-images.githubusercontent.com/80065996/153251890-47afff24-24b5-4bf3-a0a6-0756a7d8f676.png)



# we are trying to access the server running inside the container using a software installed in our server as shown in below diagram


![image](https://user-images.githubusercontent.com/80065996/153252509-42166d67-bce2-409d-8c7d-51954779317b.png)



# solution:= we have to give multiple commands like shown in below diagram to avoid this issue.


![image](https://user-images.githubusercontent.com/80065996/153253414-8fa116b8-9164-44f7-8073-7dec75c9eef8.png)


# Now we can see how to issue second command to a running container. ('Docker exec' command)



![image](https://user-images.githubusercontent.com/80065996/153254000-d14723bf-2f98-49f8-a08c-d4cffb525f2e.png)


# 'Docker exec' command used to get inside of the running container and we can issue commands to avoid "connection refuse" error when we access application running inside
# container from outside of the container


![image](https://user-images.githubusercontent.com/80065996/153254889-6cc207d3-851d-41e0-8f8f-03743db382ca.png)


# now we are inside of the container and we are able to use the redis server with redis-cli as shown below


![image](https://user-images.githubusercontent.com/80065996/153255020-9201cf0a-4c12-4fdd-b770-5dddfb8c430b.png)


# The command you are typing in the terminal will come under 'STDIN'. Positive output of a request(i.e response) showing in screen is called 'STDOUT'
# if any error occured then it will come under 'STDERR' 


![image](https://user-images.githubusercontent.com/80065996/153428484-2b5d94dd-33b7-41e5-bf80-354db569987c.png)


# The Purpose of "-it' flag in 'Docker exec' command
# if you use only '-i' flag you wont see output in a nicely formatted way. "-t' flag will give output in more formatted way
# demo:
# started redis container


![image](https://user-images.githubusercontent.com/80065996/153549073-fa13d336-f397-4bf7-b23e-23b6c6473ff5.png)


# you can see docker is waiting for input but there are no messages are anyting to indicate that we need to provide input


![image](https://user-images.githubusercontent.com/80065996/153549324-a285cbd2-f18f-4f41-9395-bae2bc8b8fbb.png)


# The same scenario when we use '-it' flag. we will get everything in more formatted way 


![image](https://user-images.githubusercontent.com/80065996/153549392-7ec8f20c-1266-4334-b4bf-f3bd2c8bb8ff.png)


# you can clearly see the difference between the two commands. '-it' flag provided some comments to indicate docker is waiting for inputs
# This is the reason we are using '-it' flag.


# Access terminal inside the container


![image](https://user-images.githubusercontent.com/80065996/153549625-735f5f0c-8d4c-4b72-8e71-cdd7503473d5.png)


# started redis container


![image](https://user-images.githubusercontent.com/80065996/153549978-67bc4e61-2b83-414a-b855-a5f7c73424f6.png)


# Open another git bash and check the running container


![image](https://user-images.githubusercontent.com/80065996/153550118-02cae7df-5082-4a65-8758-58c76e3cb5b1.png)


# now with 'sh' command we can access the terminal inside the container and can execute any commands we want
cd ~/ ==> go to home directory of the user
cd / ==> go to root


![image](https://user-images.githubusercontent.com/80065996/153550247-d5ebe46c-8afe-475e-b396-e7c5042a16ac.png)


# you can access all linux feautres. This command will help us to avoid executing 'Docker exec' command multiple times to provide commands other than start up command


# what is 'sh;


![image](https://user-images.githubusercontent.com/80065996/153550497-c789522d-37af-4249-a7e6-b7312dfeb99f.png)


# Usage of flag "-it" with the "docker run" command. 

# What will happen when we issue  "docker run -it busybox sh" 

# 1) busybox image will be downloaded from docker hub. The image will have 'file system snapshot' with 'start up command'
# 2) file system snapshot will be copied to namespace of server we are running the docker. and an empty container will be created with part of kernel,part of namspace.
# 3) that empty container will be ready to recieve command via STDIN
# 4) since we have given 'sh' with '-it' flag, the defautl start up command will be overrided with 'sh' command. the empty container will run 'sh' command and open
# the linux terminal for our work around.


# Demonstatration
# Running busybox image using '-it' flag


![image](https://user-images.githubusercontent.com/80065996/153551793-4f32e8d4-1077-402a-9d71-b0a29b3250a9.png)


# Since container is still running. we can open the another gitbash terminal and check the busybox container is runing


![image](https://user-images.githubusercontent.com/80065996/153552007-936adbc4-06ae-4baa-a0bb-d1aeacceea7e.png)


# DOCKER ISOLATION
# each docker container has its own file system. Files avialble inside one container cannot be accessed by another container. we are going to check that

# Step 1: Open 3 instances of gitbash terminal and connect to EC2 server

# Step 2: run "docker run -it busybox sh" in two of the gitbash terminal.

Terminal 1:


![image](https://user-images.githubusercontent.com/80065996/153552948-e9171b72-7c07-400f-9b27-cfa8f18effba.png)


Terminal 2:


![image](https://user-images.githubusercontent.com/80065996/153552979-2268f67b-6962-4cdd-824b-e592d401d7a5.png)


# Step 3: Open the third gitbash instance check 'docker ps' you could see 2 docker container of busybox is running shell temrinal


![image](https://user-images.githubusercontent.com/80065996/153553124-6d503413-b76b-41d1-9a4c-8799e9134ca7.png)


# step 4: Open the first gitbash terminal and create a new file using 'touch' command in the first container 


![image](https://user-images.githubusercontent.com/80065996/153553478-7c6f1962-3e2a-4785-b7b8-8ccb4609171c.png)


# step 5: open the second gitbash terminal. type 'ls' in the second container. you will not see the file 'file1.txt' in second container
# Even though containers are created in same harddisk, namespace concept will give isolation to file system of each container so that file created
# in one container will not be seen in another container.


![image](https://user-images.githubusercontent.com/80065996/153553714-a29b6884-4161-4792-90f4-a3b16c9f13b5.png)


# created a file in second container (file2.txt)


![image](https://user-images.githubusercontent.com/80065996/153553761-2b1e65f1-0073-40c6-8237-7e38f04e3a14.png)


# checking for the file (file2.txt) in the first container. it will not be present. Going to first gitbash terminal and type 'ls'


![image](https://user-images.githubusercontent.com/80065996/153553848-f2da5def-6f2f-4c53-ade2-04795e33672a.png)


# 'file2.txt' is not present as shown in above diagram. This hence proves continer will have isolation and we cannot share the filesystem


# Creating our own custom Docker image and use it for our purpose


![image](https://user-images.githubusercontent.com/80065996/153563964-0c55ced3-2293-41e2-9135-9305a77e69b6.png)


![image](https://user-images.githubusercontent.com/80065996/153564241-289c37c4-02ad-4418-b9ef-ed6d2351969c.png)


![image](https://user-images.githubusercontent.com/80065996/153564468-65c32b2e-e199-44fc-8b3b-afd352c9f49a.png)


# Follow below steps

mkdir redis-image
cd redis-image
touch Dockerfile
nano Dokerfile

===================

**Dockerfile:

# Use existing Docker image as the base 

FROM alpine

# Download and install Dependency

RUN apk add --update redis

# Tell the image what to do when empty container is started

CMD ["redis-server"]


![image](https://user-images.githubusercontent.com/80065996/153609054-635a34ad-78ff-4cd4-9f8a-3ab94b1697fb.png)



![image](https://user-images.githubusercontent.com/80065996/153608952-5883696f-aa1c-49d6-abf9-2771d8247897.png)


Building the Dockerfile created using below command

# Docker build -t name_of_the_image:Version_tag .   (Dont forgot the last dot)


![image](https://user-images.githubusercontent.com/80065996/153609475-20ba47c7-6d62-4aa8-84c0-58ae8ebd0c1d.png)


# you could see image created from the Dockerfile


![image](https://user-images.githubusercontent.com/80065996/153609606-938f0c6c-8776-4697-af33-5ab6f4d2dd50.png)


# using image id we have to create the container using 'Docker run' command


![image](https://user-images.githubusercontent.com/80065996/153610381-6f97c423-edf6-4528-bce7-0081d78cbca8.png)


# container created


![image](https://user-images.githubusercontent.com/80065996/153610438-6c962fbb-b3ac-42c9-b5a4-d2a16df2abdb.png)


# what happened here -- > File system snapshot (alpine + Apt get update command's result) copied to namespace of EC2 server and empty container has started.
# after that start up command will be executed as we mentioned using 'CMD' in Dockerfile


# Same image running without '-it' flag. Container with redis sever has started


![image](https://user-images.githubusercontent.com/80065996/153615611-4fba5964-74fa-413d-bcd4-1933021281d5.png)


# Details on Docker file


![image](https://user-images.githubusercontent.com/80065996/153616025-28d29926-145d-449c-875a-eeed53f3c5a8.png)


![image](https://user-images.githubusercontent.com/80065996/153622947-735649ac-8108-4783-8a9e-20e65d5577cd.png)


![image](https://user-images.githubusercontent.com/80065996/153623009-a7fd8284-1aa2-4ab9-ace9-6e5765f9da45.png)


![image](https://user-images.githubusercontent.com/80065996/153623305-c51f94f4-fc29-4f6c-88c9-cf06d7537215.png)


![image](https://user-images.githubusercontent.com/80065996/153623481-cc1e8a32-0548-437a-b559-3c98465b07d3.png)


# Total count of commands will be calculated by docker. so each step runs it will show as "step number/ Total step counts" as shown below


![image](https://user-images.githubusercontent.com/80065996/153625838-ec1cbce0-a00e-4e40-9647-51e19887bbe7.png)


# Intermediate container concept


![image](https://user-images.githubusercontent.com/80065996/153627033-6cdd23eb-ce8f-45d9-b7e5-6c1dd9700ba8.png)


# Steps of what is happening when we create a image using 'Docker build' command in our Dockerfile - Behind the scene process


# Step 1: Basic set up at the beginning


![image](https://user-images.githubusercontent.com/80065996/153627460-2340054c-4043-45f7-a776-bd55e59c2c86.png)


# Step 2: First statement 'From:alpine' will take file system snapshot into the namespace of EC2 server and empty container will be started
# and then second statement 'RUN' will get executed as 'running process' in container. The container started here is the intermediate container. for each step, 
# previous step will be referred and then intermediate container will be created. After the process is completed intermediate container will be deleted.
# WHEN INTERMEDIATE CONTAINER DELETED, WHATEVER STEPS EXECUTED TILL NOW WILL BE TAKEN AS NEW FILE SYSTEM SNAPSHOT SO THAT WHEN NEXT STEP RUNS IT WILL TAKE THIS LATEST
# FILE SYSTEM SNAPSHOT AND PROCESS IT.


![image](https://user-images.githubusercontent.com/80065996/153628090-10df3890-8f50-4360-b0f2-d81a5d4ad1c6.png)



# STEP3: YOU CAN SEE UPDATED IMAGE BELOW. INITIAL ALPINE FILE SYSTEM SNAPSHOT + RESULTS OF 'RUN' COMMAND (INSTALLED DEFAULT PACKAGES ALONG WITH 'REDIS')

# updated image highlighted below as result of immediate container (Container id -- below provided is sample, you can replace it as per your example)


![image](https://user-images.githubusercontent.com/80065996/153630832-5b6cf4c5-29ad-40b9-98a9-7ddcac8e5aa2.png)


# REDIS in installed as highlighted below as part of updated file system snapshot


![image](https://user-images.githubusercontent.com/80065996/153631004-e34e812f-101a-409d-85c6-0af136b94b6f.png)


# STEP 4:  container got refreshed and ready for next instruction (Intermediate container deleted)


![image](https://user-images.githubusercontent.com/80065996/153631376-3ffb9e64-1d90-4fb2-bbe3-7e42ff474200.png)


# Step 5: When step 3 ( CMD) executes, it will take file system snapshot from previous step, and then starts new container and executed the commands (CMD)
# 'CMD' has argument has 'start redis' command. since 'redis' is installed into file system snapshot as part of previous step, it will works fine now in the third step


![image](https://user-images.githubusercontent.com/80065996/153632221-2504a6f6-2cb3-4d8b-8fa5-ceee6cb0db5b.png)


# Step 6:Image will be created from the intermediate container and intermedicte container will be deleted as shown below


![image](https://user-images.githubusercontent.com/80065996/153633576-28d78703-e39c-4b42-9c6b-2ec8e2103a77.png)


# Recap of Docker image build process:


![image](https://user-images.githubusercontent.com/80065996/153704261-5a1bd125-8e89-40e7-9520-82326098938c.png)


# continution of above diagram


![image](https://user-images.githubusercontent.com/80065996/153704313-bc55735a-16a3-48f8-9476-8999b2d22063.png)


# REBUILD WITH CACHE - Concept


![image](https://user-images.githubusercontent.com/80065996/153704432-43702fe5-cb82-4ad7-9bed-1f1c1224c5c8.png)


# Adding new line in the middle of Dockerfile we have created.

# Earlier one


![image](https://user-images.githubusercontent.com/80065996/153704775-953b34eb-b201-4693-94d8-de9e387027a6.png)


# Changed one


![image](https://user-images.githubusercontent.com/80065996/153704844-8af27b61-8cd4-46f9-b3af-cbc5ff8cfa05.png)


# Since we added new step (step 3) to install gcc, Docker will create new intermediate container and take the snapshot. 
# the intermediate image created as part of first 2 steps will be presented in Docker Build cache. So by looking at the Dockerfile, Docker is very intelligent
# enough to identify the build cache and resue the same image. That is the reason Docker is so fast. 
# From this we know that any change in the middle of Docker file will create a new intermeidate image as part of build cache.


![image](https://user-images.githubusercontent.com/80065996/153705055-6de7c9c5-2de9-4094-b05c-574770b88743.png)


![image](https://user-images.githubusercontent.com/80065996/153705160-1f7825de-8562-425d-8ace-4f865c941463.png)


# running docker build again to see all the steps are used from Build cache. Because we dont have any change in the Dockerfilr


![image](https://user-images.githubusercontent.com/80065996/153705230-c2463f37-8672-45fa-aa3d-5d387cb0ca3f.png)


# image created - which has 'File system snaphot along with start up command from 'CMD'


![image](https://user-images.githubusercontent.com/80065996/153705271-d69aed65-cc36-4e7f-841e-635908abc6cc.png)


# Concept := CHANGING THE ORDER OF STEPS IN DOCERFILE. 
# whenever you change the order of steps in Dockerfile, the build cache will not be used by docker. because build cache memory will be remembered based on order of steps
# Docker executed the file. So any change in the order or the steps in Dockerfile, Docker will donwload build from the beginning it will not use cache.
# Example := changing the order


# Docker file


![image](https://user-images.githubusercontent.com/80065996/153705525-a7d2acce-215b-439f-ae47-94552b8d6ea0.png)


# Using Cache


![image](https://user-images.githubusercontent.com/80065996/153705514-cdd4c849-f58e-4913-be7c-abc6f968bd0b.png)


# Swap the Step 2 and Step 3 in the Dockerfile


![image](https://user-images.githubusercontent.com/80065996/153705622-1b291357-0a2f-41cd-8ea9-31d4b0907ce2.png)


# After swapping building the Dockerfile to create the image
# you could see from step 2 everyting runs freshly as if it is runing for the first time because it is not using build cache since order is changed
# last time when we build it, (alpine followed by redis installation will be remembered by docker and filesystem snapshot will be present in build cache)
# since we have changed order build cache will not be available


![image](https://user-images.githubusercontent.com/80065996/153705660-e60713b6-c337-4614-89c7-0a6e9f2bd741.png)


# CONCEPT - TAGGING THE IMAGE


![image](https://user-images.githubusercontent.com/80065996/153719273-fcd02f68-0d48-4039-b009-8f448deea879.png)


![image](https://user-images.githubusercontent.com/80065996/153719331-aacf215f-a767-4ede-b101-f325669df22d.png)


![image](https://user-images.githubusercontent.com/80065996/153720122-9155412f-b612-497e-b5f1-79927cf45cd2.png)


![image](https://user-images.githubusercontent.com/80065996/153720172-85dbade0-fb19-483c-89c7-555dfa3ea67e.png)


# Instead of starting the container using container id, we can use 'name of the image'. That is the main reason we are use 'tag' to provide name to the image


![image](https://user-images.githubusercontent.com/80065996/153720264-ae2900be-6b2c-4233-951c-ae6d2dcd5779.png)


# we have to provide the name in below format while using docker image we just tagged


# docker run name_of_docker_hub_profile/repo_name or project_name:version_name
# Example as per above image : "docker run sundar/redis:v1"


# Project in Docker 
# Project Outline


![image](https://user-images.githubusercontent.com/80065996/153720971-64f341cd-e8fa-49a2-aeb4-b60af7358e52.png)


![image](https://user-images.githubusercontent.com/80065996/153721017-62b833da-8f52-490f-a45f-0565019845fa.png)


# Create a directory called 'simpleWeb' and enter into that directory using 'CD' command


![image](https://user-images.githubusercontent.com/80065996/153721716-0ae6ab1c-9b66-40c6-a797-f8ee120c42fd.png)


# Create a file called 'package.json' and give the details. This file is equivalent to 'go.Mod' file in Golang


![image](https://user-images.githubusercontent.com/80065996/153721966-e9287dec-2799-49fe-bd7b-64d8dc1130a0.png)


![image](https://user-images.githubusercontent.com/80065996/153743657-1dc2c975-2ee8-4e8c-91ad-1537ce3b1d92.png)


![image](https://user-images.githubusercontent.com/80065996/153744083-02e6f18b-1e25-446c-8c75-604fd1178114.png)


![image](https://user-images.githubusercontent.com/80065996/153744717-cb0f7951-1523-41b3-811d-f92677b5fcd6.png)


![image](https://user-images.githubusercontent.com/80065996/153744736-9279d028-5bd2-4d55-be27-8c4d39c32052.png)


![image](https://user-images.githubusercontent.com/80065996/153744742-e16bd70c-1011-47ae-bf8e-0395dd7950ff.png)


![image](https://user-images.githubusercontent.com/80065996/153744749-89722558-143d-44ec-93c5-4f85432c40ac.png)


# when we try to build the dockerfile, we immediately getting error as shown below,


![image](https://user-images.githubusercontent.com/80065996/153744941-68a6696b-6878-4f6a-b6a3-f15ddb998719.png)


# Why error is occured when we try to build the Dockefile above ?

# BASE IMAGE ISSUES
**in the step2, "RUN npm install" command, as part of first step file sustem


![image](https://user-images.githubusercontent.com/80065996/153745305-659ab90e-8d21-4514-86e9-77b2b0163eb9.png)


![image](https://user-images.githubusercontent.com/80065996/153745357-08868248-628e-4ff9-b5ff-a036d27ad454.png)


# Alpine Operating system is very small. so it will not have much package manager installed. (Only 'apk' package manager will be installed by default)
# We have to install 'npm' package manager in order to use run the 'node js' applications
# We have 2 options to solve this issue,
# 1) we can use other image with 'npm' package manager installed already in it
# 2) or else we can build our own image by intalling 'npm' package manager on our own.

# for this demo, we are going to use other image which has 'npm' installed already.
# In 'Docker hub' we can see some images which has 'operating system with node package manager' installed already. we can take this and use it.


![image](https://user-images.githubusercontent.com/80065996/153745753-ade9f8b7-c943-4bd2-b358-50e7d8c600ac.png)


# similary packages will be available for all programming languages. Similar image for Golang,


![image](https://user-images.githubusercontent.com/80065996/153745844-ef5a19ef-5336-4631-83f3-630b4ba955a4.png)


# We can refer Dockerfile versions in the same page where we find the image


![image](https://user-images.githubusercontent.com/80065996/153745913-e693d2d0-1daa-4a9d-a395-03d2f576cae1.png)


# we can use any of this version along with name of the image in the dockerfile
# click the version tag(bwlo highlighted) to see usage of Dockerfile


![image](https://user-images.githubusercontent.com/80065996/153746001-16014977-6b83-4b26-831e-64c9f745de73.png)


![image](https://user-images.githubusercontent.com/80065996/153746011-4b4182ac-90d1-407e-9da0-eeedcb9af742.png)


# Given the similar construct in docker file. I am going to use 6.14 version


![image](https://user-images.githubusercontent.com/80065996/153746068-bf297f66-39d6-48fe-9b2a-bd3fc1dab1aa.png)


![image](https://user-images.githubusercontent.com/80065996/153746174-5257579e-840b-4818-b7f7-a4a50410f79a.png)


# Image crateted,


![image](https://user-images.githubusercontent.com/80065996/153746186-c439dfbe-260a-477c-9a39-fc5189a8caf2.png)


# Quick note: While creating image on our own by building docker file, startup command will be decided in the last step using 'CMD' option. so once all the steps run
# Docker image will be created with file system snapshot along with startup command at the end of all steps completed from Dockerfile using 'docker build' command
# but when we use image already present in docker hub, that means it already has file system snapshot along with start up command by default.


# there will be alpine version for every image present in Dockerub, instead of versin 6.14 of 'node' image we can use alpine version of same 'node' image which reduces
# final size of the image created.


![image](https://user-images.githubusercontent.com/80065996/153746568-99560856-ef0c-4b0d-9e74-5d8f5351a55c.png)


# Always refer the usage of alpine from Dockerhub before using it
# sometime we get 'ideal tree' error when using alpine image as show below while building Dockerfile
# mention the workdir and copy the package.json file to workdir to avoid this issue


![image](https://user-images.githubusercontent.com/80065996/153746751-05321e2d-cfde-4d96-b223-39386403b72f.png)


![image](https://user-images.githubusercontent.com/80065996/153746785-14631f03-3608-41dc-8f70-25fe2931bb5d.png)


![image](https://user-images.githubusercontent.com/80065996/153746903-84cee01f-5baf-4fda-9d9d-940c61d33e38.png)


# updated Dockerfile to solve this issue


![image](https://user-images.githubusercontent.com/80065996/153746927-1f4f8ebe-e886-4457-a08e-3fe6ca78fcd1.png)


# You can compare the size of two docker images crated below, version v1 is created using regular OS image which is very large
# version 'v2' created with alpine image which is very less in size


![image](https://user-images.githubusercontent.com/80065996/153746962-a38d3223-6846-4c2b-9f98-d41fdd510388.png)



![image](https://user-images.githubusercontent.com/80065996/153757556-1df271d8-a106-4581-bf47-beb77c4746c0.png)


![image](https://user-images.githubusercontent.com/80065996/153757622-a271cf7e-173d-40ca-b663-7d13ee3d9126.png)



![image](https://user-images.githubusercontent.com/80065996/153757930-81f0cca0-4e62-4552-babd-8e1c68bf645f.png)


![image](https://user-images.githubusercontent.com/80065996/153758169-a1eb2526-8498-4356-82ae-65b3a3026d44.png)


![image](https://user-images.githubusercontent.com/80065996/153758187-98da1521-ede7-4a22-9e57-7c472222d9d2.png)


![image](https://user-images.githubusercontent.com/80065996/153758219-55d8d4c9-2574-47df-aff5-0b62cf134e50.png)


# We are starting a container from the image we created and tagged with version 'v2'. our node app is listening on port '8080'. we can provide any port as
# first parameter and then second parameter of port number will be the one we mentioned inside the app (index.js file) to listen to.


# you can copy public ip address along with port number 8080 to see the app running inside the container


![image](https://user-images.githubusercontent.com/80065996/153758615-bbfc7b2f-d207-4622-bcdd-1452dd9f8929.png)


# First paramater of port number, we can give any number we want. But the second parameter of the port number is something we have to give the port number 
# which is mentioned inside the app or else it will be wrong. the app inside the container we cannot access it


![image](https://user-images.githubusercontent.com/80065996/153758906-6e8d87c2-f5bd-4dcc-b942-6750e24d2e2e.png)


![image](https://user-images.githubusercontent.com/80065996/153758979-e0438444-2278-49f0-84a2-353e9b17d168.png)


![image](https://user-images.githubusercontent.com/80065996/153758999-ea178f8e-471e-4443-8dde-614ea41c28b8.png)


# Demo := What will happen is there any change in 'index.js' file ? (i.e. Some code fix we have done)


# Node app is running on port 8080. From outside we are exposing it on port '8090' as given in the 'docker run' command


![image](https://user-images.githubusercontent.com/80065996/153822443-66c34cdc-f7f2-4674-be3b-9f9eaff2db83.png)


![image](https://user-images.githubusercontent.com/80065996/153822975-3b54ab60-b159-4ff9-a8b0-84b737fc24a3.png)



![image](https://user-images.githubusercontent.com/80065996/153822623-0f8d9387-355f-448c-aa19-0b345ea812fa.png)


# We are going to change the display statment of 'hi there' to 'bye there' in 'index.js' file


![image](https://user-images.githubusercontent.com/80065996/153823105-b0b35ba1-40a6-483b-ae9e-b1e3951d1400.png)


![image](https://user-images.githubusercontent.com/80065996/153823057-45b50e02-63b4-4c68-a156-fba7870659ff.png)


# now go and refresh the browser, you will still see the old message. New message is not updated in the browser


![image](https://user-images.githubusercontent.com/80065996/153823211-b0d177a5-4361-470e-9a4b-4df7d697829d.png)


# Because, when we created the image, the file system snapshot still contains old code copied into that as specified in the dockerfile using 'Copy' command.
# so we have to create a new image along with new code changes to see the updated code changed reflected in the container and the browser 


# we rebuilt the dockerfile with same image tag (sundar/nanoapp:v2) and create the image with updated code changes in index.js
# NOTE: SINCE WE HAVE DONE A SMALL CHANGE IN 'INDEX.JS' FILE, DOCKER IS CLEVER ENOUGH TO INDENTIFY THE CHANGES AND FROM THE 'COPY' STEP EVERYTHING RUN AS NEW STEP
# INSTEAD OF USING 'BUILD CACHE' AS SHOWN BELOW


![image](https://user-images.githubusercontent.com/80065996/153824087-d09e9cb4-4d11-4678-ab0c-31495f0e69c1.png)


![image](https://user-images.githubusercontent.com/80065996/153824810-b886bd8d-6faa-4fb4-9586-5e135fb898b8.png)


# starting the container with new changes


![image](https://user-images.githubusercontent.com/80065996/153824998-56387c1a-bd85-4dc2-8d02-90cf5587790f.png)


![image](https://user-images.githubusercontent.com/80065996/153825043-a1e1fd43-6cba-4388-b513-6813b6f60bfa.png)


# Result: Changed message displayed here


![image](https://user-images.githubusercontent.com/80065996/153825091-a5f5ac7f-56b5-484e-ae07-3dc7fd210d60.png)


# AVOIDING UNNECESSARY REBUILD AND AVOID CACHE BUSTING
# As we see in the previous demo, we have done only a small change in 'index.js' file. Since the 'COPY' step is just before dependency installation step (RUN npm install),
# the change is detected by docker and rebuild started. This is not a good design, for a small change we should not rebuild the image with the complete dependency

# SOLUTION: We are changing the dockerfile slightly to accomodate like below


# Old docker file:- we are going to split the 'COPY' step into 2 steps


![image](https://user-images.githubusercontent.com/80065996/153830268-51e9838c-749d-4a51-bb85-317a33e6d01a.png)


# NEW UPDATED FILE BELOW : now only package.json will be copied before 'RUN npm install' step. Project files will be copied via newly created 'COPY' step after
# 'RUN npm install' step. So if any change in code in project file (for ex: 'index.js'), Rebuild will not happen


![image](https://user-images.githubusercontent.com/80065996/153830931-a95e576a-0aa2-43a6-a0be-816b10b0f5d6.png)


![image](https://user-images.githubusercontent.com/80065996/153832290-bc481fcb-641e-4bc1-8a53-c0e135be4164.png)


![image](https://user-images.githubusercontent.com/80065996/153832376-22665a02-f9f4-45d1-9d44-0625fd5d7c5c.png)


# starting a container out of image we created


![image](https://user-images.githubusercontent.com/80065996/153832638-ad166f15-bc28-4c32-a76c-0f86f96334d8.png)


![image](https://user-images.githubusercontent.com/80065996/153832722-15e6694b-7ef4-47eb-a28e-3bd8c2290b0a.png)


![image](https://user-images.githubusercontent.com/80065996/153832768-6dee6d03-5bec-497f-9ada-1629072db14e.png)


# now changing the display message to anything random message in 'index.js' file


![image](https://user-images.githubusercontent.com/80065996/153833571-a85ac6db-33c3-46ab-ba30-c0e2c08b7f9f.png)


# Rebuilding the dockerfile. if we rebuild the docker file with '-t' (tag) flag without any version, it will take 'latest' by default as shown below


![image](https://user-images.githubusercontent.com/80065996/153834468-c6e8ef0a-bbb9-464c-abd7-56de2d96bab5.png)


# you could observe, only the COPY step of project files rebuilt newly since we have changes in the 'index.js' file. we have avoided rebuild of installing
# the dependencies by this change

# starting the container from the image


![image](https://user-images.githubusercontent.com/80065996/153834993-2c74a6e0-1371-4a04-aca5-f03ace38440e.png)


# New changes picked. The learning in this demo is - how to avoid rebuild of depenedencies by a slight change in dockerfile


# Result:


![image](https://user-images.githubusercontent.com/80065996/153835156-658db55e-fec2-4760-a14f-6620834e95d3.png)


# Rebuilding the Dockerfile with no change in anything either in project files.we can mention the tag without any version so that it will rebuild the 
# dckerfile with 'latest' tag itself


![image](https://user-images.githubusercontent.com/80065996/153840026-a02e72e5-c7aa-4490-a045-fdcdd81598b5.png)


# rebuilt the Dockerfile successfully


![image](https://user-images.githubusercontent.com/80065996/153840477-fec537ee-c473-4d5e-b064-e890948ea35e.png)



