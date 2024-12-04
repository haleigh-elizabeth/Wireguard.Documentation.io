# Wireguard.Documentation.io
Detailed description on how to install wireguard on to an ubuntu droplet 

## **Project 3 - Wireguard Docker Container**<br/>
### <ins>Step 1: Create a Droplet in DigitalOcean</ins><br/>

* Create a Digital Ocean account* Use this link to [DigitalOcean.com](https://www.digitalocean.com/?refcode=d33d59113ab6&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=CopyPaste) to sign up with your school email and Agent Miller’s credit card
* Choose the lowest price tier - $6 per month
* Create an Ubuntu droplet
* Select all of the basic options
* Choose password instead of ssh key - TulsaTime@1865edu
* Name the project - Wireguard project
* Droplet IP - 64.23.171.188

### <ins>Step 2: Install Wireguard</ins>
* SSH into the droplet by opening a terminal and typing ssh root@[ip]
* Where you would replace [ip] with the IP of your DigitalOcean Droplet
* Install the dependencies/packages needed to run docker. Commands: sudo apt install docker, sudo apt install docker-compose, sudo apt install wireguard
* Set up Wireguard using Docker Compose: 
* Create a directory for Wireguard: 
* **mkdir -p /opt/wireguard**
* **cd /opt/wireguard**
 
* Create a docker-compose.yml file: 
* **nano docker-compose.yml**
 
* Add the following configuration to docker-compose.yml: <br/>

**yaml  docker-compose.yml**<br/>
  &nbsp; GNU nano 8.1<br/>                                                        
version: '3.8'<br/>
services:<br/>
  &nbsp; wireguard:<br/>
    &nbsp;&nbsp; container_name: wireguard<br/>
    &nbsp;&nbsp; image: linuxserver/wireguard<br/>
    &nbsp;&nbsp; environment:<br/>
     &nbsp; - PUID=1000<br/>
     &nbsp;&nbsp; - PGID=1000<br/>
      - TZ=American/New_York<br/>
      - SERVERURL=45.55.41.235<br/>
      - SERVERPORT=51820<br/>
      - PEERS=pc1,pc2,phone1<br/>
      - PEERDNS=auto<br/>
      - INTERNAL_SUBNET=10.0.0.0<br/>
  &nbsp;&nbsp;  ports:<br/>
      - 51820:51820/udp<br/>
   &nbsp;&nbsp; volumes:<br/>
      - type: bind<br/>
        source: ./config/<br/>
        target: /config/<br/>
      - type: bind<br/>
        source: /lib/modules<br/>
        target: /lib/modules<br/>
   &nbsp;&nbsp; restart: always<br/>
   &nbsp;&nbsp; cap_add:<br/>
      - NET_ADMIN<br/>
      - SYS_MODULE<br/>
  &nbsp;&nbsp;  sysctls:<br/>
      - net.ipv4.conf.all.src_valid_mark=1<br/>


* Save and exit. 

* Run Wireguard: 
* **docker-compose up -d**
 
* Check logs to get the QR code: 
* docker logs wireguard 

### Test Your VPN 
#### Mobile Device 
* Open the Wireguard app and scan the QR code from the logs. 
* Before connecting: 
Visit IPLeak.net and screenshot your local IP. 
* After connecting: 
Turn on the Wireguard VPN and revisit IPLeak.net. 
* Screenshot the VPN IP to confirm it is active. 
#### Laptop 
* Find the configuration file: 
* **ls /opt/wireguard/config**
 
* Copy the .conf file to your laptop. 
* In our case the .conf file contained:

[Interface]
PrivateKey = iLwC8xbCzwVd5j9s7Et/72d6keAAVTlkmxcY/wX6Ako=<br/>
ListenPort = 518<br/>
.20<br/>
Address = 10.0.0.2/32<br/>
DNS = 10.0.0.1<br/>

[Peer]
PublicKey = P5GnsQQZk4X0KilGkKNg5ND/XZjV0KP7QDNuShSCcG4=<br/>
PresharedKey = 5X6AWptfcPEHqhgi3nVlEb6vx833rLQic/ofI4TMy5s=<br/>
AllowedIPs = 0.0.0.0/0, ::/0<br/>
Endpoint = 45.55.41.235:51820<br/>


* Import the file into the Wireguard app or CLI. <br/>
* Follow the same steps as mobile to confirm functionality using IPLeak.net. <br/>
 
 


### Screenshots:









***
Documentation Completed by: 
* Ethan Belanger
* Jalen Brown
* Talha Choudhury
* Levi Dunsmore
* Haleigh Harris
* Elise Hill
* Oliver Johnson
* Braden Lavarnway
* Steven Lu
* Nolan Miller
* Kinlee Null
* James Oakes
* Devin Pattison
* Ben Pikul
* Anastasia Reed
* Ahmed Al Shaqsi
* Ahmad Sher
* Jacob Silberfarb
* Saniya Singh
* Kenji Tratnik
* Philip Tu
* Alex Watson
* Nuraiym Zhusupbekova
