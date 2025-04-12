## 1. Installing MongoDB

```
$ sudo apt update
$ sudo apt install gnupg
$ curl -fsSL https://pgp.mongodb.com/server-6.0.asc | sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg --dearmor

$ echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

```
$ sudo apt update
$ sudo apt install -y mongodb-org
$ sudo systemctl start mongod 
$ sudo systemctl enable mongod (ensure to automatically start it on system boot)
```
## 2. Installing Open5gs
```
$ sudo add-apt-repository ppa:open5gs/latest
$ sudo apt update
$ sudo apt install open5gs

```

## 3. Installing Node.js

```
 $ sudo apt update
 $ sudo apt install -y ca-certificates curl gnupg
 $ sudo mkdir -p /etc/apt/keyrings
 $ curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg

 # Create deb repository
 $ NODE_MAJOR=20
 $ echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list

 # Run Update and Install
 $ sudo apt update
 $ sudo apt install nodejs -y

```

## 4. Web UI
```
$ curl -fsSL https://open5gs.org/open5gs/assets/webui/install | sudo -E bash -

```

===================================================================================================================================================================================================================
## Installation and setup is completed Now we have to configure it to be compatible with srsRAN

**
TIP:
In case of single node setup (srsGNB and Open5gs in same PC). `No change in IP address required just change MCC and MNC code`. 
In case of Multinode setup (srsGNB and Open5gs in different PCs). ` change the IP address where highlighted in image to IP address of Machine and MCC and MNC code`. 
**

## In case of multi-node setup we need to replace every ip shown in image with the IP address of the machine (Can get using `ip a` command)

### 1.   /etc/open5gs/mme.yaml configuration

```
 gedit /etc/open5gs/mme.yaml
 change the MNC and MCC code accordingly.(we have used 001 and 01 for MNC and MCC codes respectively)
 We have used the TAC as 7. (It should be same as srsRAN configuration)
 No change in IP address required for our setup.

**Change the Highlighted ip to the IP address of the Machine**
```
![image](https://github.com/user-attachments/assets/fc80d32e-3790-4e1f-96e0-1f7daae6405d)

### 2.    /etc/open5gs/sgwu.yaml configuration

```
 gedit  /etc/open5gs/sgwu.yaml
 No changes required in our setup
**Change the IP to IP address of machine in case of multinode setup** 
```

```
sudo Restart open5gs services
sudo systemctl rstart open5gs-*

```

### 3.   /etc/open5gs/nrf.yaml configuration

```
 sudo gedit /etc/open5gs/nrf.yaml
 change the MNC and MCC code accordingly.(we have used 001 and 01 for MNC and MCC codes respectively)
 We have used the TAC as 7. (It should be same as srsRAN configuration)
```
![image](https://github.com/user-attachments/assets/5f3f02d0-e10e-4a57-bdb9-5e1dbb0233e8)
### 4.   /etc/open5gs/amf.yaml configuration

```
 sudo gedit /etc/open5gs/amf.yaml
 change the MNC and MCC code accordingly.(we have used 001 and 01 for MNC and MCC codes respectively)
 We have used the TAC as 7. (It should be same as srsRAN configuration)
 No change in IP address required for our setup
**Change the highlighted IP with the IP address of system in case of multinode setup**
```
![image](https://github.com/user-attachments/assets/f47a4189-0913-4395-b556-40ef4e1b5fbf)

### 5.   /etc/open5gs/upf.yaml configuration

```
 sudo gedit /etc/open5gs/upf.yaml
 change the MNC and MCC code accordingly.(we have used 001 and 01 for MNC and MCC codes respectively)
 We have used the TAC as 7. (It should be same as srsRAN configuration)
 No change required In case of our setup
**Change the highlighted IP with the IP address of system in case of multinode setup**

```


![image](https://github.com/user-attachments/assets/89259622-bea6-48ef-abe3-b20f096d9602)


## Enabling NAT configuration in the machine to access Internet

```
### Enable IPv4/IPv6 Forwarding
 sudo sysctl -w net.ipv4.ip_forward=1
 sudo sysctl -w net.ipv6.conf.all.forwarding=1

### Add NAT Rule
 sudo iptables -t nat -A POSTROUTING -s 10.45.0.0/16 ! -o ogstun -j MASQUERADE
 sudo ip6tables -t nat -A POSTROUTING -s 2001:db8:cafe::/48 ! -o ogstun -j MASQUERADE

```

## Deactivate UFW firewall

```
 sudo ufw status
**if Active**
Status: active
sudo ufw disable
Firewall stopped and disabled on system startup
sudo ufw status
Status: inactive
```

## Restart all 5g services


```
sudo systemctl restart open5gs-*
```
