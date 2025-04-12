## 1. clone srsRAN project repository

If you clone repositoty at /home/ubuntu path no change in commands required else config files path may change. Check according to the location of repository.

```
git clone https://github.com/srsRAN/srsRAN_Project.git
```

## 2. build the srsGNB

```
cd srsRAN_Project
mkdir build
cd build
cmake ../
make -j $(nproc)
```

## 3. Install srsGNB

```
sudo make install

```

# Running srsDNB
```
sudo ./gnb -c <config file>

 for b210

cd /home/ubuntu/srsRAN_Project/build/apps/gnb
sudo ./gnb -c /home/ubuntu/srsRAN_Project/configs/gnb_rf_b200_tdd_n78_20mhz.yml
```

```
Change the amf addess to 127.0.0.5 and bind_addr to 127.0.0.1 in case of single node setup.
Change the amf addess to IP address of **PC(Where open5gs is installed)** and bind_addr to **IP address of local machine** in case of single node setup.
 Keep the PLMN code to 00101 and tac 7 (OR same as used in configuration of Open5gs.)
```
**Singlenode setup**

![image](https://github.com/user-attachments/assets/d4e2ac7e-c098-4beb-ac25-d7666ba218a6)

**Multinode setup**

![image](https://github.com/user-attachments/assets/3b2abf2c-d8d0-4389-9135-6c85bc26fd68)


![image](https://github.com/user-attachments/assets/155a7bb3-7058-4b50-9fa7-3091f8caad49)







