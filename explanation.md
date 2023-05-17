# Step One
Read through the README.md file in the YOLO directory & install all dependencies, npm install in both client & backend directories. Run 'npm start' to  test the app on http://localhost:3000/ & start the mongodb service, confirmed this by running the command 'sudo systemctl status mongod', Server listening on port 5000 & Database connected successfully.

 {First error was encountered,'Failed to start mongodb.service: Unit mongodb.service not found.', I had to unintsall current installation completely. I then encountered my second error 'E: Unable to locate package mongodb-org' when I tried to re-install mongodb  which was troubleshooted and resolved, successfully installing mondodb}

# Step Two
Create a Dockerfile for the client dir > create a docker container

# Step Three
Create a Dockerfile for the backend dir > create a docker container

# Step Four
Create docker-compose.yml file to orchestrate our e-commerce platform.
Pull a mongo db latest image from docker hub 

# Step Five
Add product Cynthia, check on website

# Step Six
Check if the data is persistent, it was and worked consistently.

# Step Seven

Pushed my Client and Backend images to docker hub.

 # Deploy an application to a vagrant virtual Machine using ansible

 Preriquisites

Install Vagrant in your local machine.
Install ansible in your local machine.
Install virtual box in your local machine & disable secure boot.

First thing to do is configure your vagrant file in the root directory of the application you want to deploy. In my case the yolo directory. In your vagrant file, specify the virtual machine image to pull and initiate geerlingguy/ubuntu2004 give it a host name yolo.test, a private network ip 192.168.56.0, disable the ssh insert key by setting it to false assign some memory to it around 1500mb to 2000mb will do last but not least configure an ansible provisioner so we can run our playbook with vagrant by providing the playbook to be run. In our case playbook.yaml.

We create a plabook.yaml file and populate it;

Every playbook must start with ---
we set our hosts machine to all . Thi will help ansible pick up the virtual machine that spinned up by vagrant in our virtualbox
we set become to true so we are able to run our commands as sudo in our virtual machine.
We set a pre_tasks that updates our apt cache and give it an interval of 3600 seconds. this will ensure that everytime we run our playbook, ansible will be installing the latest versions of whats defined in our plays, from our apt repository.
We set our var_tasks to point to our vars.yml file. In this file, we will declare variables to be used in our playbook.
We can now start defining our tasks. We need to configure our vm by setting up an environment to deploy our application. For that we need; a. Install the git package. This will allow us to be able to git clone our project from git hub. b. install dependancies and update cache. This are the dependancies needed to aid in installation of the various softwares we will require for the project. c. installing docker and docker-compose.
add gpg keys from docker website, then we add a docker repository to apt, then we install docker using apt by installing docker-ce, docker-ce-cli,containerd.io.
we make sure that docker is running and will run on booting by setting the state to started and enabled to yes.
Install docker compose python package by usisng ansible.builtin.pip and install the docker python module to enable ansible to run docker compose up. d. Install mongo db in our virtual machine.
import public key from mongodb.org
Add a reporitory in apt and update the apt cache
install mongodb using apt. the apt package name is mongodb-org
Ensure that mongodb is running and will run on booting by setting the state to started and enabled to yes.
By this point our virtual machine is ready to receive our containirised application and run it. We clone the repository using the ansible.builtin.git module and our destination to /usr/local/src/yolo and set our state to present. finaly we run our docker compose by setting our play as shown below

name: Run docker-compose docker_compose: project_src: /usr/local/src/yolo state: present
The last step is to check the website via the link http://192.168.56.0:3000/ add a product and confirm that the data persists.

Point to note, to run the playbook use the command vagrant up to create the VM and vagrant provision to initiate the plays.