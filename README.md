   ### How to Build Smart Code through Dockerization using CI/CD tools (Jenkins, Docker and Ansible)
                      
  
  
  ![alt text](https://github.com/tanersa/sharksJenkins/blob/master/virtualization_conterization.png)
  
  
   In short, Virtual Machines (**VMs**) are heavyweight and Containers are lightweight. **Virtualization** requires a Host Operating System (**HOS**) and a hypervisor which runs and manages one or more VMs. Additionally, each application must have a seperate Guest Operating System (**GOS**) that can be major hurdles for Software Development Life Cycle (**SDLC**) since our major goal is to find the bug as early as possible. On the other hand, **containerization** mandates only HOS and supporting files run time such as Docker. In each supporting files run time, there would be multiple applications running depends on the need of the infrastructure. 
   
   Containers only comes with neccessary components to run each application whereas virtualization needs extra layer of parts such as storage, memory and etc. which makes it heavyweight. Containers are easy to deploy, migrate, create, and kill. Creating a container takes about only 1-2 seconds. However, having a VM up and running takes about 10 min. One can run an operating system under a different operating systen through dockerization which does not exist in virtualization. For instance, ubuntu (from debian family) can be run inside redhat operating system without needed GOS.
   
   Lets say, you developed your source code and would like to test your changes in DEV environment fast. Creating and initializing a VM takes time and is hard. Here, you can create your docker container easily and deploy your application to container then start your testing in short period of time. One can create, stop, remove a container really quick. 
   
   Docker containers are **best microservices**. For example, multiple applications are deployed to docker containers. If one container fails, it doesn't affect another container. Therefore, we will be able to achieve High Availability (**HA**). 
   
   We can consider **Jenkins** as a glue for microservices which put all the components together such as nodejs, java or javascript, bootstrap, jsp files, front end parts, back end parts, Application Programming Interfaces (**APIs**), database and so on so forth. Our main goal is to find the bugs as early as possible. This is necessary to build bug free code. As soon as developers, devops team, and automation testers checks in their changes, application will be built using maven build management tool and artifacts (archieves) will be created. Then the artifacts will be deployed to target servers. 
   
   In order for Jenkins to process **CI/CD pipeline**, we will need to configure all necessary requirements on Jenkins console, so Jenkins can begin building the application and deploy to target machines. Jenkins will be able to deploy **tomcat** application on port no 8080 by default. Now, we would like to deploy our own application on browser not only the **tomcat** app. Therefore, we need to create a **Dockerfile** for deploying our custom application not only the tomcat. Futhermore, **Dockerfile** gets created under **/home/dockeradmin** directory. It will take care of everything for us such as creating docker image and container. **Dockerfiles** are definition files which defines how we would build our docker container, what we will do, where **.war** file should be deployed to. 
   
   There are two different deployments:
   
      A) Fresh Deployment
      B) Upgrade Deployment
      
   Whenever you do upgrade, you dont change the container name and port no. All you change is **configuration**. Therefore, deploying first time would give us **_SUCCESS_!**. However, deploying second time would give **UNSTABLE** result because Jenkins is trying to build a container but a docker container aleardy exsits. Hence, we have to build more **modular** code!  
   
  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
