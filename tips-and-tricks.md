# Tips and Tricks for Jetson Xavier
These are useful
## Software packages
### JetPack
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

### Python and PyTorch
Install useful Python packages

```bash
sudo apt install python3-pip libfreetype6-dev libffi-dev -y
pip3 install cython
pip3 install numpy jupyter jupyterlab matplotlib pandas
```

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

### Tools
Command line resource monitor [jetson_stats](https://github.com/rbonghi/jetson_stats). Works well in SSH.
```
sudo -H pip3 install -U jetson-stats
jtop
```

Web-based resource monitor Netdata
```
sudo apt install curl
bash <(curl -Ss https://my-netdata.io/kickstart.sh)
```
open your browser to <http://192.168.55.1:19999/>
