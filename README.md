Instance: Ubuntu-512MB-Tokyo-1
IP: 3.112.45.16
Default user: ubuntu
User: grader gr4d3r


Get your server:
1. Start a new Ubuntu Linux server instance on Amazon Lightsail. There are full details on setting up your Lightsail instance on the next page.

2. Follow the instructions provided to SSH into your server.
- Download the ssh Default key from the Amazon LightSail web.
- Edit Amazon LightSail firewall rules.
- ssh ubuntu@3.112.45.16
- ssh ubuntu@52.193.1.71

Secure your server.
3. Update all currently installed packages.
sudo apt-get update
sudo apt-get upgrade

4. Change the SSH port from 22 to 2200. Make sure to configure the Lightsail firewall to allow it.
sudo vim /etc/ssh/sshd_config
sudo service ssh restart

5. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).
sudo ufw status
Status: Inactive

sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2200/tcp
sudo ufw allow www
sudo ufw allow ntp

sudo ufw enable

ubuntu@ip-172-26-6-204:~$ sudo ufw status
Status: active

To                         Action      From
--                         ------      ----
80/tcp                     ALLOW       Anywhere
2200/tcp                   ALLOW       Anywhere
123                        ALLOW       Anywhere
22                         DENY        Anywhere
80/tcp (v6)                ALLOW       Anywhere (v6)
2200/tcp (v6)              ALLOW       Anywhere (v6)
123 (v6)                   ALLOW       Anywhere (v6)
22 (v6)                    DENY        Anywhere (v6)

6. Exit and connect: good luck.
ssh -p 2200 ubuntu@3.112.45.16
ssh -p 2200 ubuntu@52.193.1.71


sudo adduser grader
sudo cp /etc/sudoers.d/90-cloud-init-users /etc/sudoers.d/grader
sudo nano /etc/sudoers.d/grader
su grader
ssh-keygen

sudo apt-get install apache2
sudo apt-get install libapache2-mod-wsgi
sudo apt-get install postgresql
Port 5432 is denied
sudo -i -u postgres psql

sudo vim /etc/apache2/sites-available/catalog.conf
create client_secrets.json
vim webtool.wsgi
sudo a2ensite catalog
sudo service apache2 restart

CREATE USER catalog WITH PASSWORD 'p4ssw0rd';
CREATE DATABASE catalog OWNER catalog;


Install Flask (same as Vagrant machine)

Enable Google Authentication for the server´s IP

ssh_key id_rsa
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAvhc4Q62dgLPpuXEvT44+QgGgp6KyCacEf616twEYlQk7nomW
D0Ocx1EMMn39HXEiakQiRH1gSmBDzf/s+L7ERbP4DHR4YitoTttKyMcl8HC6k75b
d9y2UsPc+oMvoMgnF4jKTC6yuKmSk0dLkoOt94Pr5IYMCcj8+hchRrzcdPEW7eNd
q5QWpQWT4hoR5Fyrt6dwsm34T2FeJe0lJhZEflykyTciwvhdwUPIGS8E54hsKRe6
WppJeLV19PpPWpwfgv2vNZ12hRhnk9rNN9KdyvYgGr4rZyjCKO1F3iuMaw5yuD0a
oDjrZKflgsqZ4I8HYdwCeLOS4ylE6F+Bv64VLwIDAQABAoIBAC9cx7cNJgYwTZbX
3arbzSVTFH1QKz3+cD+DsOSyEDbqEwHAVDQ/a2u6BOj7vTo9uw5xJXydJIXDkIFe
N+QOXAbl/XLU/j2vhRDI0MxP2mMbI1G2h0HJK2BZztBYKWDNHfheK9FpfTxHe+7Y
P7sktg7Kvta0k4FIo8eIRdFDM0arcVReDLnKz+wevZ/MoEizrl1qKk5eHmXEWDvs
zioGRAW6xf1HWFvqnt4ukJ+BFWl7DP6GgMHvaxXQghIQvp9TNEEzp6X8WVrMPNUk
vCqME4PNI32omX5WmsAZp663Ecq/T9uZiuhI/B1AqtMiHEAiwF2B4L2EKDuqjFwa
5slOC2ECgYEA30d3UbWfl+yDFtxZrXSYGDHFFRrOVyEQGpMZe22fP/SgKE1VFmL6
q30OCkZCHO0P9dTaiAE9IP02mn0SI6iwa6h5JOUT/QdlM1ntML1Zsov08FNZ+6Wm
DBXySEcBwLinonAgPvXPw0rETdG1r3532LZAM/JSttXatNrX3lojN9ECgYEA2fKo
CyXjiUncv5zRNo8HlNahoRU12zinLWaxlBKKtUWix4Qn0ciXq3MkV6bYMoRFCDtR
yuq5X6X4/OJUXezPAN8U0uhb9QNDnc8jkZwAw72LUVEGGktQvsekoD11suXSlnrK
zyBS62TE0O8ScrpG9bmi457uXqpCUW0YuILcvP8CgYEAxEQF1oVYbCsyb/3xtk8v
AtV88DhH+L7PcQys8ZpCye02eza+/Ja00dlzZgSsSND5npYkIjk0irMKNHKMZ1v4
+Cl3k77p+xltE96QaK+JETGFdVtPVa0ecLE5796647VtZZQ6RB2/K2OleuJEWqdI
oe5SMVdo7d6+CQv1hTamjoECgYEAzWui6274uQt/HrLllfDVinmJudPOASOynl4u
fYvEZPqPZFGxXk8cdSJ/XIYLPAHjNtECVKlLs1UyCtggAK8UpJOegvMyyQocjv8P
XUyWg+eBClG92MaoAkkVZ1rGNqnbBK4TvYmP3gIKZ4sN7kiYXT5swvGnZl4/R5P2
OuJMv20CgYBV9QrpuheL8hf5lMaShlvE//lpxu23lJGStvVIckFRxo/pqGEX03td
YvOIqlRAq4K6wl3XEJI2cat01f0XGmI8zFi5y+O/cPgfwhqc/HySF/WUWrrVM8Fd
JgXmwyFwT9LBxrIzhxPsZj6cMNpQ33t3gqfEG8yQ6cl0ioHGi9LEXw==
-----END RSA PRIVATE KEY-----
