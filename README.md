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








