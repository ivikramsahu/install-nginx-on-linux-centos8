![how to install nginx on centos 8 , linux , rhel 8](https://i.imgur.com/zpB4yRm.png)

## Introduction 

Nginx is an open-source web server with high-performance HTTP and reverse proxy. Majority of largest sites on the internet trust Nginx for handling tons of load. 

## Usage

* Standalone web server
* Load balancer
* Content cache
* Reverse proxy for both HTTP and non-HTTP servers

As per benchmarks Nginx is capable of handling larger number of concurrent connection with smaller memory footprint per connection as compared to Apache.

## Prerequisites

* Make sure you have `sudo` privileges 
* Make sure Apache is not running or any other application using port 80 or 443.

## Installation

1) Installing nginx on centos 8

   `sudo yum install -y nginx`
   
   **OR**
   
   simply type `nginx` on the terminal 
   
   ```bash
   [root@localhost ~]# nginx
   bash: nginx: command not found...
   Install package 'nginx' to provide command 'nginx'? [N/y] y
   
   * Waiting in queue... 
   * Loading list of packages.... 
   The following packages have to be installed:
   nginx-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64	A high performance web server and reverse proxy server
   nginx-all-modules-1:1.14.1-9.module_el8.0.0+184+e34fea82.noarch	A meta package that installs all available Nginx modules
   nginx-mod-http-image-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64	Nginx HTTP image filter module
   nginx-mod-http-perl-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64	Nginx HTTP perl module
   nginx-mod-http-xslt-filter-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64	Nginx XSLT module
   nginx-mod-mail-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64	Nginx mail modules
   nginx-mod-stream-1:1.14.1-9.module_el8.0.0+184+e34fea82.x86_64	Nginx stream modules
   Proceed with changes? [N/y] y


   * Waiting in queue... 
   * Waiting for authentication... 
   * Waiting in queue... 
   * Downloading packages... 
   * Requesting data... 
   * Testing changes... 
   * Installing packages... 

   ```

    when you type `y` + enter 
    
    It will automatically install all dependecies 
    
2)  Once you have installed nginx successfully trigger the below command.

    ```bash
    sudo systemctl enable nginx
    sudo systemctl start nginx
    ```
    
3) Above command will enable and start the service you can check and verify the same using the below. 

    `sudo systemctl status nginx`
    
     **OR**
     
     `sudo service nginx status`
     
4) Output on success and failure will be shown below

  **ON Success**
  
   ```bash
   ● nginx.service - The nginx HTTP and reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
     Active: active (running) since Sun 2019-10-31 21:09:32 IST; 5min ago
   ```  
   
   **ON Failure**
   
   ```bash
   [root@localhost ~]# systemctl status nginx 
    ● nginx.service - The nginx HTTP and reverse proxy server
    Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; vendor preset: disabled)
    Active: failed (Result: exit-code) since Thu 2019-10-31 21:11:58 IST; 9s ago
   ```
    
##  Firewall Restriction

centos 8 has its predefined firewalld service with rules for HTTP {80} or HTTPS {443}

  ```bash
  sudo firewall-cmd --permanent --zone=public --add-service=http
  sudo firewall-cmd --permanent --zone=public --add-service=https
  sudo firewall-cmd --reload
  ```

if it already configure you will getting below alerts

  ```bash
  [root@localhost ~]# sudo firewall-cmd --permanent --zone=public --add-service=http
  Warning: ALREADY_ENABLED: http
  success
  [root@localhost ~]# sudo firewall-cmd --permanent --zone=public --add-service=https
  Warning: ALREADY_ENABLED: https
  success
  [root@localhost ~]# sudo firewall-cmd --reload
  success
  ```
  
   
