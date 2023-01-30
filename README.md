# JENKINS

- Jenkins Standalone Architecture

```bash
Developers commit changes           <-------------------------->
----------------------------------> | Github Repository |
                                    |       |
                                    <-------------------------->
                                    |   Jenkins server
                                    | (Build<-->Test<-->Result)
                                    |       |<----------------->
                                    |       | Deploys to Production server
                                    <-------------------------->
                                    | Production server

```

- Jenkins Distributed Architecture (Master-Slave Model)

```bash
Developers commit changes           <-------------------------->
----------------------------------> | Github Repository |
                                    |       |
                                    |       | Pulls and build
                                    <-------------------------->
                                    |   Jenkins Master server
                                    | (Build<-->Test<-->Result)
                                    |       |
                                    <-------------------------->
                                         | Jenkins Slave
                                    <--------------------------->
                                    |             |             |
                                 Windows        Linux          MacOS
```

### Minimum harware requirements:

```bash
256 MB of RAM

1 GB of drive space (although 10 GB is a recommended minimum if running Jenkins as a Docker Container)
```

### Recommended hardware configuration for a small team:

```bash
4 GB+ of RAM

50 GB+ of drive space
```

### Software requirements:

- Java: see the Java Requirements page
- web browser: see the Web Browser Compatibility page
- For Linux operating system: Linux Support Policy

```bash
cat /etc/os-release
```

```bash
PRETTY_NAME="Ubuntu 22.04 LTS"
NAME="Ubuntu"
VERSION_ID="22.04"
VERSION="22.04 LTS (Jammy Jellyfish)"
VERSION_CODENAME=jammy
ID=ubuntu
ID_LIKE=debian
NAME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="hhtps://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
UBUNTU_CODENAME=jammy
```

```bash
# Install Java
# To install latest OpenJDK 11
sudo apt install openjdk-11-jre
# To check the java version
java -version
```

```bash
# Add Jenkins APT Repository Key
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key |sudo gpg --dearmor -o /usr/share/keyrings/jenkins.gpg
# Append the Debian package repository address to the server's sources.list
sudo sh -c 'echo deb [signed-by=/usr/share/keyrings/jenkins.gpg] \ http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
# Run apt update so that apt will use the new repository
sudo apt update
```

### Install Jenkins and its dependencies:

```bash
sudo apt-get install jenkins
```

- Start Jenkins jenkins

```bash
sudo systemctl start jenkins
sudo systemctl status jenkins
```

- Opening the firewall

```bash
sudo ufw allow 8080
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status
```

- How to check Jenkins version command line in linux

```bash
grep version /var/lib/jenkins/config.xml

<?xml version='1.1' encoding='UTF-8'?>
   <version>2.332.3</version>
```

### Configure Jenkins on Ubuntu 22.04 LTS

- After install of Jenkins, successfully running Jenkins services and we will check on browser by jenkins default port number 8080.

```bash
http://ip_address_or_domain_name:8080
```

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
