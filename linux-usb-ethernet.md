# Using ethernet over USB on Linux
Source and further reading: `README-usb-dev-mode.txt`.

On Windows and Mac, the Jetson AGX Xavier should automatically get forwarded ethernet over USB.

On Linux, this needs to be manually configured to enable ipforwarding and NAT.

Use the following procedure to configure your host as a gateway for Jetson.

1. Enable IP forwarding with your host's configuration tools, or by running
   the following command as root:

   ```bash
   sudo echo 1 > /proc/sys/net/ipv4/ip_forward
   ```

   If your host system is connected to multiple networks at the same time,
   please consider any security implications of this configuration change.

   Depending on your Linux distribution, you may be able to make this change
   permanent by editing /etc/sysctl.conf.

2. Enable Network Address Translation (NAT) using your host's configuration
   tools, or by running the following command as root:

   ```bash
   sudo iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to 192.168.1.100
   ```
   
   where:
   
    `eth0` is the name of your host's upstream Ethernet interface.
    
    `192.168.1.100` is your host's IP address on that interface.
    
   These can be obtained using the command `ifconfig`
   
   ![ifconfig](https://git.its.aau.dk/WW82ZE/docs_xavier/raw/branch/master/img/ifconfig.png)

Depending on your Linux distribution, you may have to run this command every
time your host is rebooted.

You can check this in the iptables rules with
```bash
sudo iptables -t nat -L
```