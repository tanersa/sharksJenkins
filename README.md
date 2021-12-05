   ### How to Build Smart Code through Dockerization using CI/CD tools (Jenkins, Docker and Ansible)
                      
  
  
  ![alt text](https://github.com/tanersa/sharksJenkins/blob/master/virtualization_conterization.png)
  
  
   In short, Virtual Machines (VMs) are heavyweight and Containers are lightweight. Virtualization requires a Host Operating System (HOS) and a hypervisor which runs and manages one or more VMs. Additionally, each application must have a seperate Guest Operating System (GOS) that can be major hurdles for Software Development Life Cycle (SDLC) since our major goal is to find the bug as early as possible. On the other hand, containerization mandates only HOS and supporting files run time such as Docker. In each supporting files run time, there would be multiple applications running depends on the need of the infrastructure. 
   
   Containers only comes with neccessary components to run each application whereas virtualization needs extra layer of parts such as storage, memory and etc. which makes it heavyweight. Containers are easy to deploy, migrate, create, and kill. Creating a container takes about only 1-2 seconds. However, having a VM up and running takes about 10 min. One can run an operating system under a different operating systen through dockerization which does not exist in virtualization. For instance, ubuntu (from debian family) can be run inside redhat operating system without needed GOS.
   
   Lets say, you developed your source code and would like to test your changes in DEV environment fast. Creating and initializing a VM takes time and is hard. Here, you can create your docker container easily and deploy your application to container then start your testing in short period of time. One can create, stop, remove a container really quick. 
   
   
