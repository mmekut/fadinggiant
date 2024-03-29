# fadinggiant
Local Development VM

A Virtual Machine with LAMP support for development and testing built using Hashicorp Vagrant, Oracle Virtualbox and fully provisioned with Ansible automation Tool.

The VM is built with AlmaLinux 8 official box from vagrant cloud and configures the following server packages:

- Apache HTTP Server 2.4.x (with self-signed OpenSSL certificate)
- MariaDB 10.6
- PHP 8.1.x
- Nodejs v16
- Postgresql Server 13.x
- Redis
- Memcached Instance
- Composer (available globally)
- Adminer

NOTE: CentOS 8 has been decapitated by RedHat so we moved to the closest RHEL variant that is stable.

The VM is designed primarily for PHP development but contains perl, nodejs and python3 interpreters as well as gcc/make tools.

BASIC REQUIREMENTS

To run this VM, your PC must be on Windows 7 SP1 (64-bit --- though i run mine on 32-bit but it is not advisable) with powershell 3.0+, Windows 8.1 and Windows 10.

Your PC must be connected to a power supply and stable internet connection before firing up the machine.

It is highly recommended to peruse the vagrant doc at vagrantup.com/docs if you are new to vagrant and virtualization.


SET-UP

- Download and install latest Vagrant.
- Download and install latest Virtualbox (applicable to your pc architecture).
- Open powershell and use 'vagrant box add almalinux/8' command to download vagrant box.
- Clone this repo to your preferred directory OR download the zip file and unzip to your preferred directory.
- Restart your system.
- Open powershell, run cd to the root directory of the project and use 'vagrant status' command to see if vagrant and virtualbox is installed successfully.
- Open powershell and run cd to the root directory of the project. Use 'vagrant up' command to set-up the machine.
- To access the HTTP server from a browser using a name (e.g sweetgeez.local), You will need to edit your host file at windows/system32/drivers/etc/hosts with notepad running as an administrator. Then map your preferred hostname to the IP found in the vagrantfile ELSE you will be accessing the server using the IP in the vagrantfile. NOTE: Vagrant can do this automatically with the hostname plugin but I prefer doing things manually to understand the process better.



CONFIGURATION

To customize the VM configuration, open the vagrantfile and modify its content before running vagrant up command.

Ansible roles variables are found in ansible/var/all.yml. If you want to install/configure any services not included with this package, kindly look for ansible roles that configure such services on Ansible Galaxy and edit requirements.yml and playbook.yml found in ansible folder. Don't change anything you don't understand. Visit ansible docs when in doubt.

Always use the relevant docs before starting this VM OR you can use the issue queue to ask questions for clarification.


USAGE

Copy your project directory inside the 'www' folder OR create a new project directory. The 'www' folder is synced with /var/www/fading in the VM. You can create and edit your project files on your PC using your favorite IDE or text editor.

If you've edited the windows hosts file and include your preferred hostname as an entry, just type the hostname in your browser to access the HTTP Server. Else use the IP found in the vagrantfile to access the HTTP server.

You can also run "vagrant ssh" command in the powershell terminal to logged into the VM but you must know basic linux command as this is a headless linux OS.

ANY QUESTION, SUGGESTION AND REQUEST FOR HELP, PLEASE OPEN AN ISSUE.
