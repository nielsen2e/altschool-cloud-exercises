
![AltSchool Africa Logo](./images/1633989073690.jpg)

# Task: 
Setup Ubuntu 20.04 LTS on your local machine using Vagrant

## Instruction: 
<ul>
   <li>Customize your Vagrantfile as necessary with private_network set to dhcp
   </li>
   <li>Once the machine is up, run ifconfig and share the output in your submission along with your Vagrantfile in a folder for this exercise.
   </li>
</ul>

## Solution:
<ol>
   <li>Download Virtual Box (A Virtualization software that aids in the use of linux OS).
   </li>

   <li>Download Vagrant (amd64 for 64-bit computers and 686 for other processors).
   </li>

   <li>Go to your terminal (Gitbash preferably) and create a folder boxes and cd into boxes and create another folder ubuntu and cd into ubuntu.
   
   Run the following commmand:
   
```sh
mkdir boxes && cd boxes && mkdir ubuntu && cd ubuntu
```
   </li>

   <li>Initialize Vagrant using

 ```sh
Vagrant init ubuntu/focal64
``` 
ubuntu/focal64 is a box meant for the operation of ubuntu.

Vagrantfile is a configuration file that vagrant uses to run the virtual machine.
   </li>

   <li>Set-up 'dhcp' (Dynamic Host Configuration Protocol). Every computer has an ip address just like your hose address. 
   
   We configure this vagrant file so whenever we startup the virtual machine, it will automatically assign an ip address instead of you doing it yourself. Thats where dhcp comes in.
   </li>

   <li>Run `nano Vagrantfile`( Remember filenames are case sensitive. V is different from v)
   </li>

   <li>Scroll down to where you see ;
   
   "Create a private network which allows host-only access to the machine."
   
   Uncomment config.vm.network "private_network and replace 'ip' with 'type' and change the address to 'dhcp'.
   
   To save on nano: use `ctrl + O` then `ctrl X`
   
   To save on vi: Use `i` and then `:wq` 
   </li>

   <li>Run command `vagrant up`. ubuntu/focal64 will be download to the system after eeading the configuration file.
   </li>

   <li>Run `vagrant ssh` . This signfies entry into the vm. The vm running inside vagrant.
   </li>

   <li>Run ifconfig to show you all your network adapters and their ip addresses.
   
   NB: The ip address for the vm must start with 192.168 or one of the adapters must have it. You should have 3 adapters in total.
   </li>

   <li>You will most likely encounter an error after running ifconfig.
   
   Run the following command:
   
 ```sh
sudo apt install net-tools.
``` 
sudo invokes admin privileges incase you were asked are you the root user.
   </li>
</ol>

![ifconfig snapshot](./images/Ubuntu%20Snap.png)
