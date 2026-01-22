# Setting up and launching your instance
On AWS, head to EC2 and click **Launch instance**
![An image of the EC2 page](guide_images/EC2_page.png)

We will be using the **default Ubuntu** for the OS and **t3.micro** as the instance type
![An image of the OS and Instance type settings](guide_images/OS_and_instance_type.png)

Select your Key pair, then for the Network settings, make or use a security group that has these 3 rules:
- ssh rule, Source type Anywhere (0.0.0.0/0)
- HTTP rule, Source type Anywhere (0.0.0.0/0)
- Custom TCP rule, port range 3000, Source type Anywhere (0.0.0.0/0)
![An image of the Network settings](guide_images/Security_Group_Rules.png)

As soon as you have done these settings, click **Launch instance** and you should hopefully have a running instance.

# Connecting to your instance
Now that you have your instance set up, you will need to connect to it. We will connect to it via **ssh**, so a **terminal** will need to be open for these steps.

Start by clicking on the **connect** button on your Instance page.
![An image of the Instance page](guide_images/Instance_page.png)
Then click **SSH client** to view instructions for connecting to your instance.
![An image of the Connect page, on SSH client](guide_images/Connect_page.png)
Copy the **Example command** (the highlighted code in the image above), as we will use it to connect to the instance.

Now, open up your terminal. on windows it should be **git bash** and for mac **Terminal**. Now navigate to your .ssh file, you can do so by typing: `cd .ssh`, then hit enter

Next, if you haven't done so before with your SSH key, type `chmod 400 <your ssh key name>` and hit Enter to ensure the key is not publicly viewable.

Finally, paste the command you copied from the AWS Connect page and hit Enter. You will be prompted to type yes to continue.
![An image of a bash terminal connecting to an instance](guide_images/Connecting.png)

You should now be connected to your Ubuntu instance. If not, you might need to run the command again.
![An image of a bash terminal connected to an instance, it is now in Ubuntu](guide_images/ubuntu_start_up.png)

# Setting up Ubuntu
In Ubuntu, first type `sudo nano deploy-nginx.sh` to open a text editor for the script.
Now, paste these lines of code into the box:
```
#!/bin/bash
# update packages
sudo apt update -y

# upgrade packages
sudo apt upgrade -y

# get and install nginx
sudo apt install nginx -y

# restart nginx
sudo systemctl restart nginx

# enable nginx - make nginx startup process
sudo systemctl enable nginx

# get and install unzip
sudo apt install unzip -y

# get and install nodejs v20
echo install nodejs v20...
sudo bash -c "curl -fsSL https://deb.nodesource.com/setup_20.x | bash -"
sudo apt install -y nodejs
```
You can now close nano by pressing **Ctrl X**. It will prompt you if you want to save; **type: y then hit enter**.
![An image of a bash terminal using nano](guide_images/creating_start_up_script.png)
If you want, you can use `ls` to see the file and `cat deploy-nginx.sh` to confirm it worked.

Now, to run the script, we need to type `sudo chmod +x deploy-nginx.sh`, which will allow us to execute it. 
![An image of a bash terminal using the chmod command and checking it](guide_images/chmod.png)
You can use `ls -l` to see the file permissions of the file and any others. The file name should now be green, indicating that you can run it.
Finally, type in `./deploy-nginx.sh` and let it run.

# Sending and running the Sparta app .zip file to your instance
Once the script has finished running. You will need to open a new terminal and navigate to the folder where you stored the .zip file. For me, it was located in my D drive downloads folder.
You can copy the file path and `cd` into it.
Next, run this command to send the file over to your instance: `scp -1 ~/.ssh/<ssh key name> ./nodejs20-se-test-app-2025.zip ubuntu@<instance public IPv4 address>`.

To find the instance's Public IPv4 address, you will need to look back at the instance's page on AWS, as shown here: 
![An image of the instances page highlighting the Public IPv4 address](guide_images/public_IP.png)

When you enter the command, you will be prompted if you want to continue. Type yes and hit enter. When you head back to the Ubuntu terminal, if you run `ls`, you should see the zip file. 
![An image of two bash terminals showing the prosess of sending a zip file to an ubuntu instance](guide_images/sending_zip_file.png)

To run the file, we can use the same trick we used to set up Ubuntu. Type: `sudo nano deploy-sparta-app.sh` and paste this code into it 
```
#!/bin/bash

# unzip the app file
sudo unzip nodejs20-se-test-app-2025.zip

# start up the app
cd nodejs20-se-test-app-2025/app/
npm install
npm start app.js
```
Then save and exit by pressing **Ctrl X, Y, and Enter**. Same as last time, we need to make it runnable, so type in `sudo chmod +x deploy-sparta-app.sh` then `./deploy-sparta-app.sh` to run the script.

If everything ran smoothly, your Ubuntu terminal should look like this:
![An image of the Ubuntu terminal with the app running](guide_images/app_running.png)
And if you type `http://<instance public IPv4 address>:3000` in the top of your web browser, you should see this: ![An image of the app running on a web browser](guide_images/app_running_web.png)
