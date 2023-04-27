# How_to_Configure_Static_IP_on_Ubuntu
A simple Linux task on how to configure static IP on the Network Interface on a Linux (ubuntu) machine from the terminal.

# What_is_Netplan
Netplan is the default network configuration tool for managing networks in Ubuntu. It uses YAML files that are located in ***/etc/netplan/***. It supports two renderers to control network interfaces on Ubuntu based systems which are **NetworkManager** and **systemd(networkd)**. NetworkManager is mostly used on client's desktop machine as it is GUI based while systemd(networkd) is used on servers without a GUI

# Configure_Static_IP_using_NetworkManager
  Configuring the IP using a Graphical User Interface
| ![Configuring using Network Manager](https://user-images.githubusercontent.com/41688430/234799014-6f7cbfc6-f949-4506-a35f-5ae231e7efc3.PNG)  | ![Default yaml configuration file](https://user-images.githubusercontent.com/41688430/234800288-b54d701a-544a-4355-97da-8e653ce128ad.PNG) Ubuntu using NetworkManager as the renderer to control network interfaces |
| ------------- | ------------- |


# Configure_Static_IP_using_systemd(networkd)
  Configuring the IP from the terminal. Commands have to be run as root (***sudo***)
### Step1:
  #### Stop and Disable NetworkManager. ***"systemctl stop"*** and ***"systemctl disable"***
  The Network Interface can be managed either by NetworkManager or networkd, but not by both of them at the same time.
  ![Stop and disable NetworkManager](https://user-images.githubusercontent.com/41688430/234784731-15ea69d5-203e-4865-aa03-e511d2ba9e87.PNG)
  
### Step2:
  #### Create a YAML file 
  Using your editor of choice (vim, nano etc.), create the YAML file and save it in /etc/netplan
![create the yaml config](https://user-images.githubusercontent.com/41688430/234809912-18ec5492-dc15-45a0-a2dc-7b3869761f6e.PNG)
![the yaml config png](https://user-images.githubusercontent.com/41688430/234785949-4edcad72-d343-4d44-89da-9b93228622ec.png)  
1. version - version of the network configuration format 
2. renderer - make ubuntu use networkd as the renderer 
3. ethernets - device type (an ethernet card in this case. A wireless card will be ***wifis***) 
4. enp0s3 - the network interface to be statically configured 
5. dhcp4 - false. Disable dynamic ip configuration 
6. addresses - configure the ip address 
7. gateway4 - configure the default gateway 
8. nameservers - configure the dns servers


### Step3:
  #### Apply the changes ***"netplan apply"***
  ![netplan apply](https://user-images.githubusercontent.com/41688430/234805608-ffcb347f-0555-4db9-9e9a-90ce10e630d0.PNG)

### Step4:
  #### Verify the IP using ***"ifconfig"***
  ![verify the IP](https://user-images.githubusercontent.com/41688430/234808990-dded41e6-f711-4efc-8bf4-b3e5ed651e37.jpg)
  #### Verify the default gateway using ***"route -n"***
  ![verify the default gateway](https://user-images.githubusercontent.com/41688430/234809086-449887df-7d3c-4eee-a73c-b5b7829f9e94.jpg)




 

 
