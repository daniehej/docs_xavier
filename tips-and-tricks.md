# Tips and Tricks for Jetson AGX Xavier
This document contains useful software and links to documentation that we have found to be useful when working with Jetson AGX Xavier.
# Links
Nvidia Developer forum Jetson AGX Xavier topic
- https://forums.developer.nvidia.com/c/agx-autonomous-machines/jetson-embedded-systems/jetson-agx-xavier/75

Jetson Community Projects
- https://developer.nvidia.com/embedded/community/jetson-projects

Embedded Linux wiki with many further links
- https://elinux.org/Jetson_AGX_Xavier

Further links to resources
- https://forums.developer.nvidia.com/t/links-to-jetson-agx-xavier-resources-wiki/64659

# Software packages
## JetPack
Nvidia Jetson-specific components are collected in JetPack. They can be installed as Debian packages

This enables, for example, installation of all JetPack components via
the `nvidia-jetpack` metapackage. These commands on the developer kit will result in a
full JetPack install:

```bash
sudo apt update
sudo apt install nvidia-jetpack
```

To view individual packages which are part of `nvidia-jetpack`
metapackage, enter the command:

```bash
sudo apt-cache show nvidia-jetpack
```

## Python and PyTorch
Install useful Python packages

```bash
sudo apt install python3-pip libfreetype6-dev libffi-dev -y
pip3 install cython
pip3 install numpy jupyter jupyterlab matplotlib pandas
```

### PyTorch
Install PyTorch: Follow the instructions from [Nvidia forums](https://forums.developer.nvidia.com/t/pytorch-for-jetson-nano-version-1-6-0-now-available/72048)

```bash
wget https://nvidia.box.com/shared/static/9eptse6jyly1ggt9axbja2yrmj6pbarc.whl -O torch-1.6.0-cp36-cp36m-linux_aarch64.whl
sudo apt-get install python3-pip libopenblas-base libopenmpi-dev 
pip3 install Cython
pip3 install numpy torch-1.4.0-cp36-cp36m-linux_aarch64.whl
```

Install torchvision

```bash
sudo apt-get install libjpeg-dev zlib1g-dev
git clone --branch release/0.7 https://github.com/pytorch/vision torchvision
cd torchvision
sudo python3 setup.py install
```

## Tools
### jetson_stats
Command line resource monitor [jetson_stats](https://github.com/rbonghi/jetson_stats). Works well in SSH.
```
sudo -H pip3 install -U jetson-stats
jtop
```
### Netdata
Web-based resource monitor [Netdata](https://github.com/netdata/netdata)
```
sudo apt install curl
bash <(curl -Ss https://my-netdata.io/kickstart.sh)
```
open your browser to <http://192.168.55.1:19999/> to see the Netdata interface.

To disable Netdata, run 
```
systemctl mask netdata
systemctl stop netdata
```
To enable it again, use
```
systemctl unmask netdata
systemctl start netdata
```
### GPIO pins
The GPIO pins can be controlled in Python using [jetson-gpio](https://github.com/NVIDIA/jetson-gpio)

# Tech specs

### Jetson AGX Xavier module
The module itself contains the SOC and acts as the brains of the operation. Its specifications are shown in the table.

|                    | Jetson AGX Xavier module                                                                  |
|--------------------|-------------------------------------------------------------------------------------------|
| GPU                | 512\-core Volta GPU with 64 Tensor Cores                                                  |
| CPU                | 8\-core Nvidia Carmel CPU \(ARM v8\.2 64\-bit CPU, 8MB L2 \+ 4MB L3\) \(up to 2,2656GHz\) |
| Memory             | 16GB 256\-Bit LPDDR4x \| 137GB/s                                                          |
| Storage            | 32GB eMMC 5\.1                                                                            |
| DL Accelerator     | \(2x\) NVDLA Engines                                                                      |
| Vision Accelerator | 7\-way VLIW Vision Processor                                                              |
| Encoder/Decoder    | \(2x\) 4Kp60 \| HEVC/\(2x\) 4Kp60 \| 12\-Bit Support                                      |
| Size               | 105 mm x 105 mm x 65 mm                                                                   |
| Deployment         | Module \(Jetson AGX Xavier\)                                                              |

### Developer Kit interface board
In-depth specification of the port capabilities, as well as pinouts for the GPIO pins on the Developer kit board can be found in the [Carrier Board Specification](https://static5.arrow.com/pdfs/2018/12/12/12/23/1/848262/nvda_/manual/jetson_xavier_developer_kit_carrier_board_specification.pdf).

A short summary of the ports is shown in the table.

|                          | Jetson AGX Xavier Developer Kit Interface Board                                                  |
|--------------------------|--------------------------------------------------------------------------------------------------|
| PCIe x16                 | x8 PCIe Gen4/x8 SLVS\-EC                                                                         |
| RJ45                     | Gigabit Ethernet                                                                                 |
| USB\-C                   | 2x USB 3\.1, DP \(Optional\), PD \(Optional\) Close\-System Debug and Flashing Support on 1 Port |
| Camera Connector         | \(16x\) CSI\-2 Lanes                                                                             |
| M\.2 Key M               | NVMe                                                                                             |
| M\.2 Key E               | PCIe x1 \+ USB 2\.0 \+ UART \(for Wi\-Fi/LTE\) / I2S / PCM                                       |
| 40\-Pin Header           | UART \+ SPI \+ CAN \+ I2C \+ I2S \+ DMIC \+ GPIOs                                                |
| HD Audio Header          | High\-Definition Audio                                                                           |
| eSATAp \+ USB3\.0 Type A | SATA Through PCIe x1 Bridge \(PD \+ Data for 2\.5\-inch SATA\) \+ USB 3\.0                       |
| HDMI Type A              | HDMI 2\.0                                                                                        |
| uSD/UFS Card Socket      | SD/UFS                                                                                           |


## Disk Speed
The disk speed of the AGX Xavier is around 116MB/s write and 293MB/s read, if you get read speed much over that (eg. 360MB/s), then it might be the cache you are reading from.

You can perform a disk speed test using `dd` by first creating a test file and then copying it to `/dev/null`

```
dd if=/dev/zero of=testfile bs=2G count=1 oflag=direct
dd if=testfile of=/dev/null
```

## Performance Comparison
In a small AI training test which was mildly CPU-intensive, the Jetson Xavier took 17 sec per epoch, while a Intel i7-4790K with a Nvidia GTX 960 took around 11 sec per epoch. This might give an idea about the performance of the Jetson for training, however your results may differ depending on how CPU- or GPU-intensive the workload is.