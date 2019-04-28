# linux-server-configuration


## Get your server (Amazon LightSail)
  1. Log in!
  2. Create an instance and choose you region
  <img src="Assets/lightsail/1.png" width="550">
  3. Choose an instance image: Ubuntu
  <img src="Assets/lightsail/2.png" width="500">
  4. Choose your instance plan.
  <img src="Assets/lightsail/3.png" width="500">
  5. Give your instance a hostname. (In our case, FSND-PROJECT)
  6. Wait for it to start up. It's running let's use it! 
  <img src="Assets/lightsail/4.png" width="500">
  7. Click the 'connecting the ssh' button to login to instance that we've just created.
  <img src="Assets/lightsail/5.png" width="500">
  <img src="Assets/lightsail/7.png" width="500">
  8. Project time.


## Configuration Setup


1. Go to account page from your AWS account.
  <img src="Assets/configuration/1.png" width="400">
2. Download your SSH key (ex. LightsailDefaultPrivateKey-2.pem)
3. Navigate to the directory where your file is stored in your terminal.
4. Move the private key file into the folder ~/.ssh
  ```bash
  $ mv /(current_private_key_address)/udacity_key.rsa ~/.ssh/
  ```
5. Change the key permission so that only owner can read and write

```
$ chmod 600 ~/.ssh/udacity_key.rsa
```
6. Let's log into out instance with SSH

```bash
$ ssh -i ~/.ssh/lightsail_key.rsa ubuntu@18.236.152.12
```

## Secure your server.

1. Change the SSH port from 22 to 2200. 
2. Edit /etc/ssh/sshd_config file by sudo nano /etc/ssh/sshd_config
```bash
$ nano /etc/ssh/sshd_config
```
3. Change port from 22 to 2200
4. Restart SSH 
```bash
$ sudo service ssh restart
```
5. Configure the Uncomplicated Firewall (UFW) to only allow incoming connections for SSH (port 2200), HTTP (port 80), and NTP (port 123).

```bash 
$ sudo ufw status -- utf should be inactive
$ sudo ufw default deny incoming -- deny all incoming requests
$ sudo ufw default allow outgoing-- allow all outgoing requests
$ sudo ufw allow ssh
$ sudo ufw allow 2200/tcp -- allow incoming ssh request
$ sudo ufw allow 80/tcp -- allow all http request
$ sudo ufw allow 123/udp -- allow ntp request
$ sudo ufw deny 22 -- deny incoming request for port 22
$ sudo ufw enable -- enable ufw
$ sudo ufw status -- check current status of ufw
```

