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

### 1.   /etc/open5gs/mme.yaml configuration

```
 gedit /etc/open5gs/mme.yaml
 change the MNC and MCC code accordingly.(we have used 001 and 01 for MNC and MCC codes respectively)
 We have used the TAC as 7. (It should be same as srsRAN configuration)
```
![image](https://github.com/user-attachments/assets/fc80d32e-3790-4e1f-96e0-1f7daae6405d)

### 2.    /etc/open5gs/sgwu.yaml configuration

```
 gedit  /etc/open5gs/sgwu.yaml
 No changes required in our setup 
```

```
Restart open5gs services
sudo systemctl rstart open5gs-*

```

### 3.   /etc/open5gs/nrf.yaml configuration

```
 gedit /etc/open5gs/nrf.yaml
 change the MNC and MCC code accordingly.(we have used 001 and 01 for MNC and MCC codes respectively)
 We have used the TAC as 7. (It should be same as srsRAN configuration)
```
![image](https://github.com/user-attachments/assets/5f3f02d0-e10e-4a57-bdb9-5e1dbb0233e8)

