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

In earlier releases of Docker and with the variations between Operating Systems, we had to configure the .env file with specific CONFIG and ANSIBLE_HOME entries.  *This step should no longer be necessary*

If you find that you cannot login as the ansible user with the password of password and the config files exist as per the Validation section, then update both of these entries according to your environment -

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

You should then be able to run the following in your command prompt or terminal, directly from the diveintoansible-lab directory -

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

### Troubleshooting Common Issues

#### 1. Cannot log in as the ansible user

When the lab environment is configured and started, it reads the configuration directory and sets up the ansible user.  This is based on the entry in config/guest_name.  It expects the config directory to be provided as a volume using the CONFIG entry in the .env file.  See the 'Configuration' section above as this will vary for Windows, Linux and Mac OS X.  

If this entry is incorrect, it will not find the config directory and subsequently, the ansible user will not be created.

A convenient way of verifying that the path you're using is correct is by running a similar command to the following, substituing the path you're trying to use.  If you see the output of 'ansible', the configuration path is as expected, if not, you'll need to tweak the configuration -

```
docker run --rm -v /Users/james/diveintoansible-lab/config:/config ubuntu cat /config/guest_name
```

This command passes the volume mount manually (-v for volume), the local path (/Users/james/diveintoansible-lab/config), the target mount point (:/config).  Then, it runs a ubuntu container with a command to show the contents of /config/guest_name.  Finally, --rm cleans up the container after it exits.

Lastly, the ANSIBLE_HOME entry within .env should use the same format.

#### 2. WSL with Ubuntu and exit code 255

When using Ubuntu with WSL, this issue is a result of the WSL Ubuntu image not having systemd.  It is a stripped down version of Ubuntu. The containers, all leverage systemd and when they try to use the parents subsystem this is missing.   We can work around this by just creating the components that are needed, prior to the execution of ```docker-compose up```

```
sudo mkdir -p /sys/fs/cgroup/systemd
sudo mount -t cgroup -o none,name=systemd cgroup /sys/fs/cgroup/systemd
```

This will need to be executed once every time the system is rebooted.  Rather than making permanent changes, I recommend that in these cases, a quick shell script is created to start the lab with these commands, followed by ```docker-compose up```

### Extra step for Linux users

Owing to the permissions model for Docker with Linux, there is one additional step that needs to be carried out.  With the lab working and connectivity working as ansible, perform the following actions -

```
su - 
<enter the password of password when prompted>
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
