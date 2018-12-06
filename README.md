# Server details
- Instance: Ubuntu-512MB-Tokyo-1
- IP: 52.193.1.71
- SSH is hosted on non-default port
- Key-based SSH authentication is enforced
- Root cannot login remotely.

# Steps performed:
## 1. Start a new Ubuntu Linux server instance on Amazon Lightsail. There are full details on setting up your Lightsail instance on the next page.
- Done

## 2. Follow the instructions provided to SSH into your server.
- Download the ssh Default key from the Amazon LightSail web.
- Edit Amazon LightSail firewall rules.

## 3. Update all currently installed packages.
- `sudo apt-get update`
- `sudo apt-get upgrade`
- `sudo apt-get dist-upgrade`

## 4. Change the default SSH port. Make sure to configure the Lightsail firewall to allow it.
- `sudo vim /etc/ssh/sshd_config`
- `sudo service ssh restart`

## 5. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
- `sudo ufw status`
Status: Inactive

- `sudo ufw default deny incoming`
- `sudo ufw default allow outgoing`
- `sudo ufw allow 2200/tcp`
- `sudo ufw allow www`
- `sudo ufw allow ntp`

- `sudo ufw enable`

> ubuntu@ip-172-26-6-204:~$ sudo ufw status
> 
> Status: active
> 
> To                         Action      From
> --                         ------      ----
> 80/tcp                     ALLOW       Anywhere
> 
> 2200/tcp                   ALLOW       Anywhere
> 
> 123                        ALLOW       Anywhere
> 
> 80/tcp (v6)                ALLOW       Anywhere (v6)
> 
> 2200/tcp (v6)              ALLOW       Anywhere (v6)
> 
> 123 (v6)                   ALLOW       Anywhere (v6)
>

## 6. Deploy the WebApp:
### 6.1. Create user grader:
- `sudo adduser grader`
- `sudo cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader`
- `sudo nano /etc/sudoers.d/grader`
- `su grader`
- `ssh-keygen`

### 6.2. Install Apache2, PostgreSQL:
- `sudo apt-get install apache2`
- `sudo apt-get install libapache2-mod-wsgi`
- `sudo apt-get install postgresql`
- Port 5432 is denied

### 6.3. Create user and database
- `sudo -i -u postgres psql`
	- `CREATE USER catalog WITH PASSWORD 'p4ssw0rd';`
	- `CREATE DATABASE catalog OWNER catalog;`

### 6.4. Create WSGI app
- `vim flaskapp.wsgi`
- `sudo vim /etc/apache2/sites-available/catalog.conf`
- `sudo a2ensite catalog`
- `sudo a2dissite 000-default`
- `sudo service apache2 restart`
- Download the code from GIT repository
- Create client_secrets.json
- Install python flask packages (same as Vagrant machine)