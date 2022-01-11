Minecraft 1.18 Ubuntu Server Documentation

Ubuntu Server OS

First things first a few things need to be installed.

OpenSSH Server Client:
~sudo apt install openssh-server

Enable SSH Server:
~sudo systemctl enable –now ssh

Enabled the firewall in the system:
~sudo ufw allow ssh

Install Net-tools to obtain server IP Address:
~sudo apt install net-tools -y

Check for IP address:
~ifconfig

Record your IP Address in the ‘inet’ tab (second line)
~inet XXX.XXX.X.XXX
~inet6 XXXXXXXXX

Install Screen a terminal application that can run your server in the background.
~sudo apt install screen

Install the latest version of Java Developer Kit. Since there is no gui, the server needs the “headless” version. (17 is the latest version upon writing this).
~sudo apt install openjdk-17-jdk-headless -y

Otherwise when the sudo command is needed, the new user can not put in a password since it did not have one assigned to.

At this point. I would advise two things:
Download or install an SSH client - instructions are here
I could NOT get a virtual box to copy and paste from the main machine. So be warned that typing out a link letter by letter on a black screen does not help.

Create a User named Minecraft:
~sudo useradd -r -m -U -d /opt/minecraft -s /bin/bash minecraft


Don’t log into the new server yet.
Give User minecraft a password so that you can use nano for it later:

~sudo passwd minecraft

Now log-on to the new user that was just created:
~sudo su - minecraft
*Type your password*

Create multiple parent directories
~mkdir -p ~/{backups,tools,server}

Move to the ‘server’ directory
~cd server

Get the server.jar file from Mojang’s website *NOTE do not forget to type in ‘nogui’ at the end of the command*:
~wget -O minecraft_server.1.18.1.jar https://launcher.mojang.com/v1/objects/125e5adf40c659fd3bce3e66e67a16bb49ecc1b9/server.jar 
Attempt to run the server : 
~java -Xmx1024M -Xms1024M -jar minecraft_server.1.18.1.jar nogui

NOTE the value in the front is the MAX amount of ram it is allowed to use. The second value is for the minimum amount of ram (recommended is 3GB if you plan on putting in plugins buts to get it started for now let’s use 1 Gig

Server will fail to load however you will see there are new things added
~ls

Edit the eula.txt text file
~nano eula.txt
Change the contents of the file:
eula=true
Save with: Left CTRL + X
Verify the save with: Y
To save the name as is: ENTER.

Open this file - nano ~/server/server.properties
Add/Change the following to these values: 
rcon.port=25575
enable-rcon=true
rcon.password=STRONG-PASSWORD
server-ip=(IP ADDRESS listed earlier)

To run Biomes Add the following
level-type=default

Run the java server:
~java -Xmx1024M -Xms1024M -jar minecraft_server.1.18.1.jar nogui
 
Wait for the Prepared Spawn area to complete which will take a few minutes depending on your server setup. To those who have a great writing core speed, I'm jealous.

Once the server is loaded try going into your world.
It will be just a regular world that the server genearted. There are some things you can modify now that you're in the world.

First let's get familiar with some things.
In the server terminal while the game is running. Use the OP command to set your player character as the Admin player.
~/op [Username}

Now you should be able to make some changes to the server from within the game itself. While you will still need the server running in the background. Anything that can be handled in the OS can be handled from within the game itself. For instance banning players, changing game mode, and things along those lines.

Now I need to figure out how to install plugins into the server and get it running with the server.


