## Visit this website for details
https://open-cells.com/index.php/uiccsim-programing/

### 1. Download source-code

https://open-cells.com/d5138782a8739209ec5760865b1e53b0/uicc-v3.3.tgz


Now Extract the downloaded file.

### 2. Writing sim

#### 1. go to uicc directory

```
cd uicc-v3.3
```

#### 2. Build to latest version

```
make

```

#### 3. Insert the card in the reader and the reader in a USB socket as

![image](https://github.com/user-attachments/assets/11b3b981-74c1-4cf1-b320-51839f879fe6)

#### 4. Reading the sim

```
sudo ./program_uicc

```

![image](https://github.com/user-attachments/assets/39ebf8cc-3136-410e-a175-b7d6a72d8c04)


#### 5. Write the sim

```
sudo ./program_uicc --adm 12345678 --imsi 001010000000001 --isdn 00000001 --acc 0001 --key 6874736969202073796d4b2079650a73 --opc 504f20634f6320504f50206363500a4f -spn "OpenCells01" --authenticate --noreadafter

same key and operator key we have used while creating user in Open5gs.
```

