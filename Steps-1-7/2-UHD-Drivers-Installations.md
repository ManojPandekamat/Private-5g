### UHD Drivers are required to connect the srsRAN with the B210 USRP Server to wireless mobile phones.

👉 B210 act as a tower or (Base stations) in our 5g setup.

## Install dependencies

```
sudo apt-get install cmake make gcc g++ pkg-config libfftw3-dev libmbedtls-dev libsctp-dev libyaml-cpp-dev libgtest-dev
```

## Install UHD drivers

```
sudo add-apt-repository ppa:ettusresearch/uhd
sudo apt-get update
sudo apt-get install libuhd-dev uhd-host
```

## Installing the reqired images for USRP B210.

```
sudo uhd_images_downloader
```

# Now Connect the B210 device to PC in which you want to install srsRAN and check if your device detects B210

```
uhd_find_devices
```
```
uhd_usrp_probe
```

It will print the device if B210 is detected.

![Uploading image.png…]()
