   ### How to Build Smart Code through Dockerization using CI/CD tools (Jenkins, Docker and Ansible)
                      
  
  
  ![alt text](https://github.com/tanersa/sharksJenkins/blob/master/virtualization_conterization.png)
  
  
   In short, Virtual Machines (**VMs**) are heavyweight and Containers are lightweight. **Virtualization** requires a Host Operating System (**HOS**) and a hypervisor which runs and manages one or more VMs. Additionally, each application must have a seperate Guest Operating System (**GOS**) that can be major hurdles for Software Development Life Cycle (**SDLC**) since our major goal is to find the bug as early as possible. On the other hand, **containerization** mandates only HOS and supporting files run time such as Docker. In each supporting files run time, there would be multiple applications running depends on the need of the infrastructure. 
   
   Containers only comes with neccessary components to run each application whereas virtualization needs extra layer of parts such as storage, memory and etc. which makes it heavyweight. Containers are easy to deploy, migrate, create, and kill. Creating a container takes about only 1-2 seconds. However, having a VM up and running takes about 10 min. One can run an operating system under a different operating systen through dockerization which does not exist in virtualization. For instance, ubuntu (from debian family) can be run inside redhat operating system without needed GOS.
   
   Lets say, you developed your source code and would like to test your changes in DEV environment fast. Creating and initializing a VM takes time and is hard. Here, you can create your docker container easily and deploy your application to container then start your testing in short period of time. One can create, stop, remove a container really quick. 
   
   Docker containers are **best microservices**. For example, multiple applications are deployed to docker containers. If one container fails, it doesn't affect another container. Therefore, we will be able to achieve High Availability (**HA**). 
   
   We can consider **Jenkins** as a glue for microservices which put all the components together such as nodejs, java or javascript, bootstrap, jsp files, front end parts, back end parts, Application Programming Interfaces (**APIs**), database and so on so forth. Our main goal is to find the bugs as early as possible. This is necessary to build bug free code. As soon as developers, devops team, and automation testers checks in their changes, application will be built using maven build management tool and artifacts (archieves) will be created. Then the artifacts will be deployed to target servers. 
   
   In order for Jenkins to process **CI/CD pipeline**, we will need to configure all necessary requirements on Jenkins console, so Jenkins can begin building the application and deploy to target machines. Jenkins will be able to deploy **tomcat** application on port no 8080 by default. Now, we would like to deploy our own application on browser not only the **tomcat** app. Therefore, we need to create a **Dockerfile** for deploying our custom application not only the tomcat. Futhermore, **Dockerfile** gets created under **/home/dockeradmin** directory. It will take care of everything for us such as creating docker image and container. **Dockerfiles** are definition files which defines how we would build our docker container, what we will do, where **.war** file should be deployed to. 
     
   **_There are two different deployments:_** 
   
    A) Fresh Deployment
    B) Upgrade Deployment
      
   Whenever you do upgrade, you dont change the container name and port no. All you change is **configuration**. Therefore, deploying first time would give us **_SUCCESS_!**. However, deploying second time would give **UNSTABLE** result because Jenkins is trying to build a container but a docker container aleardy exsits. Hence, we have to build more **modular** code! We need to fix this issue. Consequently, we have to build more DevOps tools and we need better Container Orhestration. Then, **Ansible** **(Configuration Management Tool)** comes into the picture. There is no master in Ansible where we can pull all configuration. We need to configure everything manually. **Ansible** also has hosts file which is called **'Inventory'** file. **Inventory** file contains target machine **Internet Protocols** (**IPs**). Inventory files would be found under **/etc/ansible** directory.
   
   From **Ansible**, we are going to ping these machines and do our deployment from  **Ansible** to all these target machines. Furthermore, another component of **Ansible** tool is **_Ansible Playbook_** file which is in yaml format. **Ansible Playbook** file is located under **/opt/docker/** directory. In this playbook file, we basically direct ansible to find the hosts file which is our inventory file for the deployment and do deployment to these target machines. Next lines in **_Ansible Playbook_**, ansible copy module should be used to give direction where **webapp.war** file will be copied from and where it should be placed to. 
   
   **tasks:**

  - name: Copy file with owner and permissions
    ansible.builtin.copy:\
      src: /opt/docker/webapp.war\
      dest: /opt/docker\
      owner: ansadmin\
      group: ansadmin\
      mode: '0644' 
   
   
   Then all the necessary steps should be taken as below:
   
   **_Stopping current container_** 
  - name: stop current running container\
    command: docker stop simple-devops-container\
    ignore_errors: yes 

   **_Removing stopped container_** 
  - name: remove stopped container \
    command: docker rm simple-devops-container \
    ignore_errors: yes

   **_Removing docker image_** 
  - name: remove docker image \
    command: docker rmi simple-devops-image \
    ignore_errors: yes

   **_Building docker images_**
  - name: Build Docker image using war file\
    command: docker build -t simple-devops-image .\
    args:
      chdir: /opt/docker

   **_Creating a new container_**
  - name: Create container using simple-devops-image \
    command: docker run -d --name simple-devops-container -p 8080:8080 simple-devops-image
    
    Finally, we can build jenkins job one more time and look at the logs. It should give us success output in normal circumstances since we are stopping and removing our instances and removing our images before creating new ones. By doing this, we achieve smart code deployment using **Ansible**. 
    
#### Dockerhub Leverage:

   We also leveraged **Dockerhub** registry as a repository because we prevent storing our images locally. If one of VMs goes down, we do not want to loose our docker images. We rather prefer to keep docker images in centralized location.
   
   Below are the commands that needs to be run in cli for dockerhub registry:
   
   1- **_Tag your images_**:
   
   docker tag (docker-image-name) (docker-user-id / docker-image-name)
   
      Example: docker tag simple-devops-image sharksdocker/simple-devops-image
   
   2- **_Login to Docker Account_**:
   
   docker login 
   _Username and password will be prompted for the user_
   
   3- **_Push your image to docker hub_**
   
   docker push (docker-user-id / docker-image-name)
    
      Example: docker push sharksdocker/simple-devops-image
    
   4- **_Login to your Docker account and verify your docker image on your acc._**
    
   Note[^1].
   [^1]:If you would like to pull your docker image from dockerhub, simply replace 'push' flag with 'pull' then run your cli command.
    
      Example: docker pull sharksdocker/simple-devops-image:latest
   
   
   
   
   

   
   
   
   
  
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
