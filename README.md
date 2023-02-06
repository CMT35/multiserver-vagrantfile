###This Vagrantfile sets up two virtual machines, "web1" and "db_M", using VirtualBox as the provider.

For the "web1" virtual machine:

1. uses the "ubuntu/bionic64" box as the base image.
2. sets up a private network with IP address "192.168.56.16".
3. configures the virtual machine with 2 CPUs and 1024 MB of memory.
4. provisions the virtual machine using an inline shell script. The script performs the following tasks:
     i. Updates the package repository
     ii. Installs Apache2, Wget, and Unzip.
     iii. Starts and enables the Apache2 service
     iv. Downloads a zip file from the internet, unzips it, and copies the contents to the Apache2 default document root.
      v. Restarts the Apache2 service.
      
      
For the "db_M" virtual machine:

1. uses the "geerlingguy/centos7" box as the base image.
2. sets up a private network with IP address "192.168.56.20".
3. configures the virtual machine with 2 CPUs and 1024 MB of memory.
4. provisions the virtual machine using an inline shell script. The script performs the following tasks:
      i. Installs the MariaDB database server.
      ii.Starts and enables the MariaDB service.
      iii. Creates a database named "wordpress".
      iv. Grants privileges to a user named "wordpress" with password "TESTING123".
       v.Flushes the privileges.
