# docker-project

## WordPress-Docker-Compose
        "WordPress is a factory that makes webpages"[14] is a core analogy designed to clarify the functions of WordPress: it stores content and enables a user to create and publish webpages, requiring nothing beyond a domain and a hosting service.
       WordPress is free and open source blogging tool. it also a content management system based on PHP and MySQL , which runs on a web hosting service. Features include a plugin architecture and a template system, referred to within WordPress as Themes.
                   WordPress is used by more than 60 million websites,[5] including 33.6% of the top 10 million websites as of April 2019,[6][7] WordPress is one of the most popular content management system solutions in use.
          
## MySQL :          
          MySQL is an open-source relational database management system . MySQL is free and open-source software under the terms of the GNU General Public License, and is also available under a variety of proprietary licenses. MySQL was owned and sponsored by the Swedish company MySQL AB, which was bought by Sun Microsystems.
          MySQL is a component of the LAMP web application software stack , which is an acronym for Linux, Apache, MySQL, Perl/PHP/Python. MySQL is used by many database-driven web applications, including Drupal, Joomla, phpBB, and WordPress. MySQL is also used by many popular websites, including Facebook,Flickr,MediaWiki, Twitter,and YouTube.
                  
## Build with following :
     1 . RedHat Linux (RHEL8)
     2 . Docker
     3 . MYSQL
     4 . wordpress
## By using this repository :
     1 . pull images from DockerHub
     2 . docker pull mysql
     3 . docker pull wordpress:5.1.1-php7.3-apache
     4 . yum install mysql & wordpress:5.1.1-php7.3-apache
     
## Docker Installation on Redhat(RHEL8) :
![redhat](https://user-images.githubusercontent.com/44314055/81595939-e3add880-93e0-11ea-8c0c-5ad7084c7b80.png)

  - Login as root to configure :
    - command to go to root account -> su -
  - Configuration of yum :
    - it is not configured by default .
      - First we have to go to yum.repos.d :
           
            gedit /etc/yum.repos.d/root.repo
      - in root.repo:
      
            [dvd1]
            baseurl = file:///run/media/root/RHEL-8-0-0-BaseOS-x86_64/AppStream
            gpgcheck = 0


            [dvd2]
            baseurl = file:///run/media/root/RHEL-8-0-0-BaseOS-x86_64/AppStream
            gpgcheck = 0
    - After : 
       
            yum repolist
            
  - Configuration of yum for docker : 
    - in docker.repo :
            [docker]
            baseurl = https://download.docker.com/linux/centos/7/x86_64/stable/
            gpgcheck = 0
  - Configure yum by adding docker.repo and root.repo inside the /etc/yum.repos.d for local installation.
    Next , run command yum install docker-ce --nobest
## To Start Docker services :
  - $ sudo systemctl start docker
   
  - After installation of the above :
    - sudo systemctl start docker
    - sudo systemctl enable docker
## Download the following Images from docker hub to use :
  - docker pull mysql:5.7 -> image for mysql
  - docker pull wordpress:5.1.1-php7.3-apache -> image for wordpress
  ## MYSQL service started :
  ![sql_1](https://user-images.githubusercontent.com/44314055/81587321-801dae00-93d4-11ea-815c-44ee05b7f18d.png)
  ## Yum install MYSQL & IP's :
  ![sql_2](https://user-images.githubusercontent.com/44314055/81594373-697c5480-93de-11ea-81e0-52f52e961b16.png)
  ![sql_3](https://user-images.githubusercontent.com/44314055/81594642-e0195200-93de-11ea-83be-8c4a52771167.png)
  ![sql_entrypoint](https://user-images.githubusercontent.com/44314055/81595145-9aa95480-93df-11ea-84e4-f2519d08885e.png)


  
## Then create the Volumes :
  - wordpress: wp_storage
    - docker volume create wp_storage
  - db: mysql_storage
    - docker volume create mysql_storage
## Create volumes for MYSQL & Wordpress :
   ![sql_create volume](https://user-images.githubusercontent.com/44314055/81594973-58801300-93df-11ea-99e7-f5417a340eb3.png)

    
## The MySQL setup :
        docker -d -it -e MYSQL_ROOT_PASSWORD=(....password....) -e MYSQL_USER=(..username..) -e MYSQL_PASSWORD=(..password..) -e MYSQL_DATABASE=(..database_name..) --name dbos mysql:5.7
       
## To Avoid the loss of data in MYSQL server we need database :
![sql_database_attach](https://user-images.githubusercontent.com/44314055/81595598-5b2f3800-93e0-11ea-853f-6a3780f5efe1.png)


## The Wordpress setup : 
        docker run -dit -e WORDPRESS_DB_HOST=dbos -e WORDPRESS_DB_USER=chirag -e WORDPRESS_DB_PASSWORD=[..password..] -e WORDPRESS_DB_NAME=mydb -v wp_storage:/var/www/html --name wpos --link dbos wordpress:5.1.1-php7.3-apache
   
#### Find ip :
  - command :
    - ifconfig
    
## Wordpress:5.1.1-php7.3-apache :
![2020-05-11 (2)](https://user-images.githubusercontent.com/44314055/81597385-4902c900-93e3-11ea-8c15-3fd54b93c42b.png)

        
## Installing of Docker-Compose-File :
  - https://docs.docker.com/compose/install
        
  - To download the current stable release of Docker Compose.
    - $ sudo curl -L "https://github.com/docker/compose/releases/download/1.25.5/docker-compose-$(uname -s)-$(uname -m)" -o      /usr/local/bin/docker-compose
                
    - To Test the installation :
      - $ docker-compose --version docker-compose version 1.25.5
                
      - In my case the file is :
        - docker-compose.yml        
                
## Running of Docker Compose:                
  - Go to the directory where is your docker compose yml file located :
    - cd command.
    - docker-compose up
  - images will be pulled if they are not availabel there.         
    - then go to port where PAT is set of you wordpress you will able to access the wordpress site.
    - For stop docker compose :
      - docker compose down
      
      
                     
