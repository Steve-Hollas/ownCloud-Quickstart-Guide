**ownCloud Quickstart Guide**

Steve Hollas

**Version 1.0, March 17, 2019**

Introduction
============

ownCloud includes the ownCloud server, which runs on Linux, client applications
for Microsoft Windows, Mac OS X and Linux, and mobile clients for the Android
and Apple iOS operating systems.

ownCloud is the most straightforward way to sync and share your data. You don’t
need to worry about where or how to access your files. With ownCloud all your
data is accessible on all devices, any time, where ever you are.

This document provides a quick overview of how you can install and configure
your ownCloud server.

This guide describes:

-   How to install and configure an ownCloud server

-   How to enable users to connect to the ownCloud server using the server IP
    address and port 8080

-   How users can connect to the ownCloud server using desktop and mobile
    clients

-   How to add user accounts

There are many ways to install an ownCloud server. The information provided in
this document is for reference only and may vary depending upon your
installation environment and requirements. Please refer to the current editions
of ownCloud manuals, which are always available online at
[doc.owncloud.com](https://doc.owncloud.com/server/).

Prerequisites
=============

Please refer to the [ownCloud Administration
Manual](https://doc.owncloud.com/server/admin_manual/) for detailed information
regarding the prerequisites and ownCloud files to install.

Install and Configure
=====================

When the ownCloud prerequisites are fulfilled and all ownCloud files are
installed, you can complete the installation by running the Installation Wizard
as follows:

1.  Point your web browser to http://localhost/owncloud.

2.  Enter your desired administrator’s username and password.

3.  Click "Finish Setup".

You’re now finished and can start using your new ownCloud server.

Installing with Docker
----------------------

ownCloud can be installed using Docker, using the official ownCloud Docker
image. This official image is designed to work with a data volume in the host
filesystem and with separate MariaDB and Redis containers. The configuration:

-   exposes ports 8080, allowing for HTTP connections

-   mounts the data and MySQL data directories on the host for persistent
    storage

Installing on a Local Machine
-----------------------------

Create a new project directory and download docker-compose.yml from [the
ownCloud Docker GitHub
repository](https://github.com/owncloud-docker/server.git) into that new
directory. Next, create a .env configuration file, which contains the required
configuration settings. Only a few settings are required:

| **Setting Name** | **Description**           | **Example** |
|------------------|---------------------------|-------------|
| OWNCLOUD_VERSION | The ownCloud version      | latest      |
| OWNCLOUD_DOMAIN  | The ownCloud domain       | localhost   |
| ADMIN_USERNAME   | The admin username        | admin       |
| ADMIN_PASSWORD   | The admin user’s password | admin       |
| HTTP_PORT        | The HTTP port to bind to  | 8080        |

Then, you can start the container using your preferred Docker command-line tool.
The example below shows how to use [Docker
Compose](https://docs.docker.com/compose/).

\# Create a new project directory

mkdir owncloud-docker-server

cd owncloud-docker-server

\# Copy docker-compose.yml from the GitHub repository

wget
https://raw.githubusercontent.com/owncloud-docker/server/master/docker-compose.yml

\# Create the environment configuration file

cat \<\< EOF \> .env

OWNCLOUD_VERSION=10.0

OWNCLOUD_DOMAIN=localhost

ADMIN_USERNAME=admin

ADMIN_PASSWORD=admin

HTTP_PORT=8080

EOF

\# Build and start the container

docker-compose up -d

When the process completes, check that all the containers have successfully
started by running docker-compose ps. If they are all working correctly, you
should expect to see output similar to that below:

Name Command State Ports

server_db_1 /usr/bin/entrypoint/bin/s … Up 3306/tcp

server_owncloud_1 /usr/local/bin/entrypoint … Up 0.0.0.0:8080-\>8080/tcp

server_redis_1 /bin/s6-svscan /etc/s6 Up 6379/tcp

In it, you can see that the database, ownCloud, and Redis containers are
running, and that ownCloud is accessible via port 8080 on the host machine.

Connecting to the ownCloud Server
=================================

You can share one or more files and folders on your computer, and synchronize
them with your ownCloud server. Place files in your local shared directories,
and those files are immediately synchronized to the server and to other devices
using the ownCloud Desktop Sync Client, Android app, or iOS app. To learn more
about the ownCloud desktop and mobile clients, please refer to their respective
manuals:

-   [ownCloud Desktop Client](https://doc.owncloud.com/desktop/latest/)

-   [ownCloud Android App](https://doc.owncloud.com/android/)

-   [ownCloud iOS App](https://doc.owncloud.com/ios/)

Logging In
----------

To login to the ownCloud UI,
open [http://localhost:8080](http://localhost:8080/) in your browser of choice,
where you will see the ownCloud login screen:

[./media/image1.png](./media/image1.png)
========================================

User Management

On the User management page of your ownCloud Web UI you can:

-   Create new users

-   View all of your users in a single scrolling window

-   Filter users by group

-   See what groups they belong to

-   Edit their full names and passwords

-   See their data storage locations

-   View and set quotas

-   Create and edit their email addresses

-   Send an automatic email notification to new users

-   Delete them with a single click

-   The default view displays basic information about your users

Please refer to [User
Configuration](https://doc.owncloud.org/server/10.1/admin_manual/configuration/user/user_configuration.html)
for detailed information.

Creating a New User
-------------------

To create a user account:

-   Enter the new user’s **Login Name** and their initial **Password** (cannot
    be "0")

-   Optionally, assign **Groups** memberships

-   Click **Create**

![](media/f251a2641131c527dec609519dabbb56.png)

Login names can contain letters (a-z, A-Z), numbers (0-9), dashes (-),
underscores (_), periods (.) and at signs (\@). After creating the user, you can
fill in their **Full Name** if it is different than the login name, or leave it
for the user to complete.

Select **Send email to new user** in the lower left sidebar on the control panel
and enter the new user’s email address. ownCloud will automatically send them a
notification with their new login information. 
