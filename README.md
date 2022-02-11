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


