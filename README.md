# Linux-Server-Project

## Introduction:
This project will access, secure, and perform the initial configuration of a bare-bones Linux server. The endpoint is the installation and configuration of a web and database server hosting my Medication Review web application.

    - Server IP address: http://34.201.120.164
    - SSH port: 2200

  - The complete URL to your hosted web application.
       - http://34.201.120.164/login

  - Softwares you installed.
    1. python 2.7
    2. Apache2
    3. Sqlalchemy
    4. Flask
    5. git
    6. PostgreSQL
    7. libsqlite3-dev
    8. mod-wsgi
    9. Fail2Ban
    10. Python OAuth2 authentication
    11. python-dev
    12. nginx
    13. httplib2

  - Below is the list of any third-party resources used of to complete this project.
      - Google OAuth2

## Update Server app
    - sudo apt-get update
    - sudo apt-get upgrade

## Install and configure automatic upgrade
    - sudo apt-get install  unattended-upgrades

    # configuration of automatic upgrades
      - cd /etc/apt/apt-conf.d
      - sudo vim 50unattended-upgrades
            - Ensure that only security update is unchecked
      - sudo vim 10periodic
              - update - APT::Periodic::Download-Upgradeable-Packages "1";
              - update - APT::Periodic::AutocleanInterval "7";
              - Add - APT::Periodic::unattended-Upgrade "1";

      - source ~/.bashrc    # to restart

## Add user grader
    - sudo adduser grader
    - give grader sudo privileges
      - sudo vim /etc/sudoers.d/grader
        # add the line below
        grader ALL=(ALL:ALL)  NOPASSWD:ALL
        # save and close the file

## Configure SSH
    # on local machine terminal, generate the ssh keys
    - ssh-keygen
      # enter the path to file and name of the file
        ~/.ssh/grader
        ## enter passphrase twice
      # copy the public key i.e grader-pub
        - cat ~/.ssh/grader-pub

    # on the server, paste the ssh public key
      # first switch to grader home directory
      - su - grader
      - mkdir .ssh
      - sudo vim .ssh/authorized_keys
        # paste the public key on this file
        # save and close the file
      # change directory and file privileges
       - chmod 700 .ssh
       - chmod 644 .ssh/authorized_keys
      # Configure the ssh login
        # open the configuration file
          - sudo vim /etc/ssh/sshd_config
            # Update the follow configuration
              # change Port from 22 to 2200
              # change PermitRootLogin to no
              # change PasswordAuthentication to no
            # save and close the file
      # restart ssh service
        - sudo service ssh restart

## Configure server Uncomplicated Firewall
    - sudo ufw status
    - sudo ufw default deny incoming
    - sudo ufw default allow outgoing
    - sudo ufw allow ssh
    - sudo ufw allow www
    - sudo ufw allow 123/udp
    - sudo ufw deny 22
    - sudo ufw enable
    - sudo ufw status

# Major applications and Softwares
  ## Install Apache2
    - sudo apt-get install apache2
    - sudo apt-get install libapache2-mod-wsgi python-dev
      # Enable Apache2
        - sudo a2enmod wsgi
        - sudo service apache2 start

    ## Instill Git
    - sudo apt-get install github



  ## Install and configure PostgreSQL with user catalog
      - sudo adduser catalog
      - sudo apt-get install postgresql
       # switch to postgresql using standard postgresql's progres users
        - su - progres
        - psql
          # give user catalog database privileges
            - CREATE USER catalog WITH PASSWORD '<enter your password>';
            - ALTER USER catalog CREATEDB;
            - CREATE DATABASE catalog WITH OWNER catalog;
            - \c catalog  ## change to user catalog
            - REVOKE ALL ON SCHEMA public FROM public;
            - GRANT ALL ON SCHEMA public TO catalog;
            - \du
            - \q   ## to switch back to progres users
            - exit  ## to exit postgresql




## App Implementation :
This is a `RESTful` web application implemented on Python framework Flask incorporating `Google` third party `OAuth authentication`. Registered users can view, edit and delete medication categories and medications created by them while unregistered user can only view the medication categories and medication within each category.

## Operating Instruction:
    - From the browser connect to the server using the URL:
        - http://54.174.85.133/login
    - Sign in with google email account to access the Web App.
    - Trasverse and enjoy the Web app

[Github link](https://github.com/jocoder22/Linux-Server-Project.git)

Useful Resources and References:
  - [Amazon Lightsail](https://aws.amazon.com/)
  - [Google Developers](https://developers.google.com/)
  - [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps)
  - [DigitalOcean Fail2ban tutorial:](https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-ubuntu-14-04)
  - Special thanks to [Steve  Wooding](https://github.com/SteveWooding/fullstack-nanodegree-linux-server-config/blob/master/README.md) for gracious README.md
