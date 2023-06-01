---
title: How we deployed Matherator using DigitalOcean
date: 2022-11-14 20:00:00 +0700
categories: [Articles, Technical]
tags: [technical]
image:
  path: /assets/img/screenshots/matherator/2022-11-13-151543.png
  alt: An ESMTE collaboration project (Thailand)
---

# Initial Setup

Before we can do any real work, we have to setup our VPS and DNS Records first.
With DigitalOcean, we can use their 1-Click App to help deploy our rails app easily.
To get started, create a DigitalOcean Droplet through their app marketplace and
point your DNS Address Records to the specified IP Address.
Make sure to point both your Apex Domain and www Subdomain, simply to be cultural.
With all of the above ready, you should be able to SSH into your brand new server.

# 1 Update the server

In our experiences, it is best to restart the VPS first before running any additional commands,
such as updating. On Ubuntu, we use the following commands:

```sh
# Restart the VPS first before running any additional commands
systemctl reboot
# Fetch the latest version of available packages
apt update
# Download and Install the available packages
apt upgrade
# Restart the VPS after making changes to the system
systemctl reboot
```

# 2 Configure Rails Parameters

We have to modify both our path for the default rails app and our rails working directory.
In this case, we prefer to use Vim as our standard editor, so make edits as follows.

![Vim Commands](/assets/img/screenshots/matherator/2022-11-13-141903.png)

![/etc/nginx/sites-available/rails](/assets/img/screenshots/matherator/2022-11-13-144524.png)
_/etc/nginx/sites-available/rails_

![/etc/systemd/system/rails.service](/assets/img/screenshots/matherator/2022-11-13-144710.png)
_/etc/systemd/system/rails.service_

# 3 Configure Rails User

To give rails user the permissions they needed, add them to the group sudo.
After that, run **sudo -i -u rails**:

![Add them to the group sudo](/assets/img/screenshots/matherator/2022-11-13-142059.png)

# 4 Clone Software Repository

Clone our desired software repository into our home folder, Matherator in this case.

![Clone our desired software repository into our home folder](/assets/img/screenshots/matherator/2022-11-13-142203.png)

Then, give the project read and write permissions.

![Give the project read and write permissions](/assets/img/screenshots/matherator/2022-11-13-142330.png)

# 5 Install Ruby and Bundler Packages

Go into our project and do an RVM Install.

![Go into our project and do an RVM Install](/assets/img/screenshots/matherator/2022-11-13-142550.png)

Then, install bundler and all of the remaining packages.

![Install bundler and all of the remaining packages](/assets/img/screenshots/matherator/2022-11-13-142712.png)

# 6 Create and Migrate Databases

As with any other web application, we need to create and migrate databases.

![Create and migrate databases](/assets/img/screenshots/matherator/2022-11-13-142833.png)

Then, proceed to restart the server, since there are a lot of changes being made.

![Restart the server](/assets/img/screenshots/matherator/2022-11-13-142953.png)

# 7 Allow requests from the domain

If we try accessing our application through the domain, an error will show up,
indicating that the hosts are blocked.

![An error will show up](/assets/img/screenshots/matherator/2022-11-13-143326.png)

The solution is to add hostname parameters to the rails environment variables.
There are many ways to achieve this, one of the recommended ways is editing
the development.rb file, which exists under the environments directory.

![Add hostname parameters to the rails environment variables](/assets/img/screenshots/matherator/2022-11-13-151020.png)

But since we like to do stuff the easy way, editing the application.rb file
is a quick and dirty way to manage variables.

![Edit the application.rb file](/assets/img/screenshots/matherator/2022-11-13-150925.png)

![config/application.rb](/assets/img/screenshots/matherator/2022-11-13-150724.png)
_config/application.rb_

Problem solved! Now we can access our application without it yelling at us.

![Problem solved!](/assets/img/screenshots/matherator/2022-11-13-151543.png)

But there's still one little problem...

Our connection to the application is not secure, meaning that it is unencrypted.
So Let's Encrypt, shall we? (Pun Intended)

# 8 Encrypting the connection with Certbot

"Certbot is a tool that automates the process of getting a signed certificate
via Let’s Encrypt to use with TLS" (Edward Angert). Start by initializing one with the following command:

![Init certbot with the following command](/assets/img/screenshots/matherator/2022-11-13-154054.png)

It will then asks for your data and permissions, make sure to read before accepting.
After that, you will have to enter in your domain names to be used with certbot.

![Enter in your domain names to be used with certbot](/assets/img/screenshots/matherator/2022-11-13-154306.png)

And there's a problem, init? Read the error message and set the server name directive accordingly.

![Error Message](/assets/img/screenshots/matherator/2022-11-13-154720.png)
_Error Message_

![Setting the server name directive](/assets/img/screenshots/matherator/2022-11-13-153554.png)
_Setting the server name directive_

Then, proceed to start certbot again, with the same parameters as last time:

![Start certbot again](/assets/img/screenshots/matherator/2022-11-13-154917.png)

![Set connection rules](/assets/img/screenshots/matherator/2022-11-13-155014.png)

It will then asks for your needs, so as always, take your time to decide.

![Decide on your needs](/assets/img/screenshots/matherator/2022-11-13-155114.png)

And Congratulations! Now everything is up and running.
Let's check our connection properties in the browser to be sure.

![Encryption Victory!](/assets/img/screenshots/matherator/2022-11-13-155840.png)
_Encryption Victory!_

Thank you, from the Matherator Team.
