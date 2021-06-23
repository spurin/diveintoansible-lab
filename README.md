## Dive Into Ansible Course Lab

Lab configuration for DiveInto.com's 'Dive Into Ansible' course

The related code repository is available at - https://github.com/spurin/diveintoansible

At present the course is available on Udemy at [https://www.udemy.com/course/diveintoansible](https://www.udemy.com/course/diveintoansible/?referralCode=28BBB7A1DCCD01BBA51F) and will be published by Packt on other platforms like O'Reilly towards the end of December 2020 or January 2021.

If you experience any problems with the lab, please reach out to me direct, James Spurin, or flag an issue in the repository

### Installation of Docker and Docker-Compose

The lab environment, makes use of Docker with Docker Compose.  If you're on Windows or Mac, you can install the convenient
Docker Desktop to make both Docker and Docker-Compose available

Linux, will require the installation of Docker and Docker Compose

### Download and Preparation

I recommend that the lab environment is downloaded to your respective home directory, i.e. -

* Mac     - /Users/james/diveintoansible-lab
* Windows - C:\Users\james\diveintoansible-lab
* Linux   - /home/james/diveintoansible-lab

On a Mac or Linux system, you should be able to clone the repository accordingly from a terminal whilst in your home directory with the following command -

```git clone https://github.com/spurin/diveintoansible-lab.git```

On Windows, if you don't have git installed, the lab can be downloaded using the following url - https://github.com/spurin/diveintoansible-lab/archive/master.zip

After unzipping the archive, you must ensure that a single diveintoansible-lab folder is copied into your home directory (not multiple folders, i.e. diveintoansible-lab-master/diveintoansible-lab or diveintoansible-lab/diveintoansible-lab).  See the next section on Validation.

### Validation (IMPORTANT)

Please verify that all of the lab files, are in the expected locations after either cloning, or extracting the zip file, for your corresponding OS and User.  They should be similar to the following -

Mac OS X -

```
/Users/james/diveintoansible-lab/.env
/Users/james/diveintoansible-lab/DiveIntoAnsible_Cover.png
/Users/james/diveintoansible-lab/README.md
/Users/james/diveintoansible-lab/docker-compose.yaml
/Users/james/diveintoansible-lab/config/guest_name
/Users/james/diveintoansible-lab/config/guest_passwd
/Users/james/diveintoansible-lab/config/guest_shell
/Users/james/diveintoansible-lab/config/root_passwd
```

Windows -

```
C:\Users\James\diveintoansible-lab\.env
C:\Users\James\diveintoansible-lab\DiveIntoAnsible_Cover.png
C:\Users\James\diveintoansible-lab\README.md
C:\Users\James\diveintoansible-lab\docker-compose.yaml
C:\Users\James\diveintoansible-lab\config\guest_name
C:\Users\James\diveintoansible-lab\config\guest_passwd
C:\Users\James\diveintoansible-lab\config\guest_shell
C:\Users\James\diveintoansible-lab\config\root_passwd
```

Linux -

```
/home/james/diveintoansible-lab/.env
/home/james/diveintoansible-lab/DiveIntoAnsible_Cover.png
/home/james/diveintoansible-lab/README.md
/home/james/diveintoansible-lab/docker-compose.yaml
/home/james/diveintoansible-lab/config/guest_name
/home/james/diveintoansible-lab/config/guest_passwd
/home/james/diveintoansible-lab/config/guest_shell
/home/james/diveintoansible-lab/config/root_passwd
```

### Configuration

Inside the diveintoansible-lab directory is a hidden file called .env that needs to be edited with a text editor.  Whilst this file contains a lot of information, it is only the CONFIG and ANSIBLE_HOME entries that need to be customised.  

Please use the following as references for each operating system accordingly, changing the username to match your own -

Mac OS X -

```
# Shared config volume
CONFIG=/Users/james/diveintoansible-lab/config

# Shared home directories
ANSIBLE_HOME=/Users/james/diveintoansible-lab/ansible_home
```

Windows (n.b. 'users' and the username (in my case this is james) are in lowercase, this is important) -

```
# Shared config volume
CONFIG=/host_mnt/c/users/james/diveintoansible-lab/config

# Shared home directories
ANSIBLE_HOME=/host_mnt/c/users/james/diveintoansible-lab/ansible_home
```

Linux -

```
# Shared config volume
CONFIG=/home/james/diveintoansible-lab/config

# Shared home directories
ANSIBLE_HOME=/home/james/diveintoansible-lab/ansible_home
```

### Running the lab

Once you've made these changes, you should then be able to run the following in your command prompt or terminal, directly from the diveintoansible-lab directory -

```
docker-compose up
```

If all goes well, it should start the lab environment.  The lab is ready for use when you see text similar to the following -

```
Attaching to docker, centos1, ubuntu2, ubuntu3, centos2, centos3, ubuntu-c, ubuntu1, portal
```

Keep this terminal open and running whilst using the course.  In your browser, then browse to http://localhost:1000 and you should get the lab interface.  If you find that you cannot login to the Ansible control host (ubuntu-c) as ansible and the password of password, then there is a fault with your configuration.  If this is the case, it is important to perform the following actions before troubleshooting or changing your configuration.  Press CTRL-C, then run the following -

```
docker-compose rm
```

Should you encounter issues at this stage that you cannot resolve, please contact me or, raise an issue in the repository with as much detail as possible (including copies of your .env file)

### Extra step for Linux users

Owing to the permissions model for Docker with Linux, there is one additional step that needs to be carried out.  With the lab working and connectivity working as ansible, perform the following actions -

```
su - <enter the password of password>
chown ansible /shared
exit
```

### Lab commands

To refresh the images with the latest course images -

```
docker-compose pull
```

To remove the lab

```
docker-compose rm
```

![DiveIntoAnsible Cover](DiveIntoAnsible_Cover.png?raw=true "Dive Into Ansible")
