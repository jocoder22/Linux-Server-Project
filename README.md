# Linux-Server-Project

## Introduction:
This project will access, secure, and perform the initial configuration of a bare-bones Linux server. The endpoint is the installation and configuration of a web and database server hosting my Medication Review web application.

    - Server IP address: http://54.174.85.133
    - SSH port: 2200

  - The complete URL to your hosted web application.
       - http://54.174.85.133/login

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

## App Implementation :
This is a `RESTful` web application implemented on Python framework Flask incorporating `Google` third party `OAuth authentication`. Registered users can view, edit and delete medication categories and medications created by them while unregistered user can only view the medication categories and medication within each category.

## Operating Instruction:
    - From the browser connect to the server using the URL:
        - http://54.174.85.133/login
    - Sign in with google email account to access the Web App.
    - Trasverse and enjoy the Web app

[Github link](https://github.com/jocoder22/Linux-Server-Project.git)
