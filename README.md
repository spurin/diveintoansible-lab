## Dive Into Ansible Course Lab

Lab configuration for DiveInto.com's 'Dive Into Ansible' course

If you experience any problems with the lab, please reach out to me direct, James Spurin, or flag an issue in the repository

### Installation of Docker and Docker-Compose

The lab environment, makes use of Docker with Docker Compose.  If you're on Windows or Mac, you can install the convenient
Docker Desktop to make both Docker and Docker-Compose available

Linux, will require the installation of Docker and Docker Compose

### Download and Preparation

I recommend that the lab environment is downloaded to your respective home directory, i.e. -

* Mac     - /Users/james/diveintoansible-lab
* Windows - /Users/james/diveintoansible-lab
* Linux   - /home/james/diveintoansible-lab

On a Mac or Linux system, you should be able to clone the repository accordingly from a terminal whilst in your homedirectory with the following command -

```git clone https://github.com/spurin/diveintoansible-lab.git```

On Windows, if you don't have git installed, the lab can be downloaded using the following url - https://github.com/spurin/diveintoansible-lab/archive/master.zip

After unzipping the archive, it is important to rename the folder from 'diveintoansible-lab-master' to 'diveintoansible-lab'

### Configuration

Inside the diveintoansible-lab directory is a file called .env that needs to be edited with a text editor.  Please use the following as references for each
operating system, accordingly, changing the username to match your own -

Mac OS X -

```
# Shared config volume
CONFIG=/Users/james/diveintoansible-lab/config

# Shared home directories
ANSIBLE_HOME=/Users/james/diveintoansible-lab/ansible_home
```

Windows (n.b. 'users' in lowercase is important) -

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

If all goes well, it should start the lab environment.  You should keep this window open and running, whilst using the course.  In your browser, then browse to http://localhost:1000 and you should get the lab interface.  If you find, that you cannot login to the Ansible control host (ubuntu-c) as ansible and the password of password, then there is a fault with your configuration.  If this is the case, perform the following actions before troubleshooting or changing your configuration -

```
docker-compose down
docker-compose rm
```

Should you encounter issues at this stage that you cannot resolve, please contact me or, raise an issue in the repository

### Extra step for Linux users

Owing to the permissions model for Docker with Linux, there is one additional step that needs to be carried out.  With the lab working and connectivity working as ansible, perform the following actions -

```
su - <enter the password of password>
chown ansible /shared
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
