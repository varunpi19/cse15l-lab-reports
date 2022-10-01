## Remote Access

# Part 1: Visual Studio Code

To download and install Visual Studio Code on your computer, go to https://code.visualstudio.com and follow the directions there. There are variations for all the popular operating systems, including Windows and OSX (for Macs) (for PCs):

![image](https://user-images.githubusercontent.com/74624958/193379576-d0ac3c02-c154-4959-bf60-37bda71cd568.png)


You should be able to open a window that look somewhat like this once it is installed:

![image](https://user-images.githubusercontent.com/74624958/193379586-207319a2-2ba7-407e-a914-6b2987251e76.png)


# Part 2: Remotely Connecting

In this section, whenever you see a chunk of code in bold, we are specifying that the code block is running on the remote server while code in italics signify it is running on your own computer. For example:

  **$ this is a command to the remote server**
  
  *$ this is a command on your own computer*
  
---
  
Course-specific accounts are used in several CSE courses. These are comparable to accounts you might obtain on different platforms at different organizations (or a future job). We'll demonstrate how to connect to a remote machine through the Internet and do tasks there using VScode/terminal.

If you're using Windows, you must take the following first step: Install the OpenSSH software so that your computer may communicate with other devices that have this kind of account. Only the OpenSSH client should be installed; the server should not be.

![Setup OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse)

You might also already have the OpenSSH Client installed on your computer. Go to 'App and Features', select 'Optional Features' and search for 'Open SSH Client'. If you see this then you need not install anything:

![image](https://user-images.githubusercontent.com/74624958/193379978-4f40998a-6ce7-4f1c-b03f-2f7def5f3d41.png)

Then, using the remote option in Visual Studio Code, we will establish a connection to the remote computer. We are referring to the procedures in the "Connect to a remote host" stage as our guide.

---

Start by opening a terminal in VSCode using the keyboard shortcuts Ctrl or Command +'or the Terminal New Terminal menu item. The letters from your course-specific account will be used in place of the fh in your command

*$ ssh cs15lfa22fh@ieng6.ucsd.edu*

(That should read one, five, l (not one); in certain typefaces, the one and l are nearly identical.)

You will probably see a message similar to this one as this is probably your first time connecting to this server:

*⤇ ssh cs15lfa22fh@ieng6.ucsd.edu
The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])?*

---

When he first connect to a new server, Our professor, Joe, always says yes to these messages because it is expected to get that message in that situation. If you encounter this message when attempting to connect to a service that you frequently use, it may indicate that someone is attempting to monitor or manage the connection. This response does a good job of describing what's happening: Answer from Ben Voigt

Therefore, enter yes and hit enter, then type your password. Once you have logged in and entered your password, the entire interaction should look something like this:

*# On your client
⤇ ssh cs15lfa22fh@ieng6.ucsd.edu
The authenticity of host 'ieng6-202.ucsd.edu (128.54.70.227)' can't be established.
RSA key fingerprint is SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting (yes/no/[fingerprint])? 
Password:*

**# Now on remote server
Last login: Sun Jan  2 14:03:05 2022 from 107-217-10-235.lightspeed.sndgca.sbcglobal.net
quota: No filesystem specified.
Hello cs15lfa22fh, you are currently logged into ieng6-203.ucsd.edu

**You are using 0% CPU on this system

**Cluster Status 
Hostname     Time    #Users  Load  Averages  
ieng6-201   23:25:01   0  0.08,  0.17,  0.11
ieng6-202   23:25:01   1  0.09,  0.15,  0.11
ieng6-203   23:25:01   1  0.08,  0.15,  0.11

Sun Jan 02, 2022 11:28pm - Prepping cs15lfa22**

Should resemble this:

![image](https://user-images.githubusercontent.com/74624958/193383068-909b469d-09fe-444f-af0f-ca51d9e72842.png)

(The number of users, load and avergaes will vary)

Any commands you issue will now be executed on the computer in the CSE basement via your terminal.  Based on how you are connected, we refer to your computer as the client and the computer in the basement as the server.

# Step 3: Run Some Commands

Try a few different iterations of the cd, ls, pwd, mkdir, and cp commands on both your computer and the remote computer after using ssh.

Here are some specific useful commands to try:

cd ~
cd
ls -lat
ls -a
ls <directory> where <directory> is /home/linux/ieng6/cs15lfa22/cs15lfa22abc, where the abc is one of the other group members’ username
cp /home/linux/ieng6/cs15lfa22/public/hello.txt ~/
cat /home/linux/ieng6/cs15lfa22/public/hello.txt
  
For example:
  
  ![image](https://user-images.githubusercontent.com/74624958/193383961-42e2a88f-ddb5-4079-804b-0d04792f2151.png)

  'ls -a' lists all files in the 'a' directory.

You can use: to log out of the remote server in your terminal- 

* Ctrl-D
* Run the exit command.

Additionally, you may create extra terminal windows in VSCode by clicking the tiny Plus button at the top of the terminal window.
  

# Step 4: Moving Files over SSH with scp
  
We've seen how to work on both local and remote computers thus far. Being able to transfer files across computers is a necessary step in remote work. There are several ways to accomplish this; in the past, you may have sent yourself an email, stored the file in Google Drive or Dropbox, and then accessed it from a different computer.
  
*class WhereAmI {
  public static void main(String[] args) {
    System.out.println(System.getProperty("os.name"));
    System.out.println(System.getProperty("user.name"));
    System.out.println(System.getProperty("user.home"));
    System.out.println(System.getProperty("user.dir"));
  }
}*
  
Compile and run the WhereAmI program using the javac and java commands below.
  
*javac WhereAmI.java*
 
*java WhereAmI*

Do you see anything? (Skip this step if java isn't already installed on your PC.)

Then, run the following command in the terminal using your username from the directory where you created the file:
 
*scp WhereAmI.java cs15lfa22fh@ieng6.ucsd.edu:~/*

Then, log into ieng6 with ssh again, and use ls. You should see the file there in your home directory! Now you can run the program on the ieng6 computer using the same javac and java commands from before.
 
**javac WhereAmI.java
java WhereAmI**
  
Since java is installed on the server, anyone should be able to run it no matter the client.
  
---
  
![image](https://user-images.githubusercontent.com/74624958/193384345-fca4e805-a0d4-4d96-84cd-6597925aadea.png)

![image](https://user-images.githubusercontent.com/74624958/193384367-e150fe69-35fb-4bd6-9eba-7bbded09a358.png)

  
The directory changed from my personal files into the cs15 account, which caused a difference in the output when running on the client. The system files for getProperty were overwritten into the components of the remote server as a result of the change in directly.
  
It personally took me around 20 minutes to get get the intial stuff started, but the password change took way longer.
  
Copying the file from my computer to the remote one didn't take me very long. When I execute the file on my computer, the operating system displays as Windows, my computer's username, and the fact that I am utilizing a desktop folder are all displayed. The information on the remote computer is entirely different because it is being opened from a completely other location. This implies that getProperty's output is entirely dependent on the context in which it is used. It took a total of 30 seconds to update the file on my laptop, sign in  and run it.
  
# SSH Keys
  
So far, we've seen how to use ssh and scp to log in, execute commands, and copy files to a remote server. We must type or copy-paste our password each time we launch scp or log in. This is time-consuming, frustrating, and prevents us from finishing the task at hand. Naturally, we should investigate whether there are any configuration or program options that could help us avoid this tiresome, repetitive activity.
  
*# on client (your computer)
$ ssh-keygen
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/joe/.ssh/id_rsa): /Users/joe/.ssh/id_rsa
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /Users/joe/.ssh/id_rsa.
Your public key has been saved in /Users/joe/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:jZaZH6fI8E2I1D35hnvGeBePQ4ELOf2Ge+G0XknoXp0 joe@Joes-Mac-mini.local
The key's randomart image is:
+---[RSA 3072]----+
|                 |
|       . . + .   |
|      . . B o .  |
|     . . B * +.. |
|      o S = *.B. |
|       = = O.*.*+|
|        + * *.BE+|
|           +.+.o |
|             ..  |
+----[SHA256]-----+*
  
![image](https://user-images.githubusercontent.com/74624958/193384418-828335b4-66db-4421-9e69-ef38a427ff04.png)

![image](https://user-images.githubusercontent.com/74624958/193384435-140bb376-9cbc-4fac-a0de-e3446b672a25.png)

Note: Press enter once again to specify the default path when prompted Enter file in which to save the key (/Users/joe/.ssh/id rsa) and make a note of it. The default location in this scenario is /Users/joe/.ssh/id rsa.

If you're using Windows, go to https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh keymanagement#user-key-generation and complete the additional ssh-add instructions there.

This produced two new files on your system: the private key (in a file named id rsa) and the public key (in a file named id rsa.pub), both of which were saved in the computer's .ssh directory.

Now, we must copy the public key—not the secret one—to the server's user account's .ssh directory.
  
*# on client
$ ssh cs15lfa22zz@ieng6.ucsd.edu
<Enter Password>*
  
**# now on server
$ mkdir .ssh
$ <logout>**
  
*# back on client
$ scp /Users/joe/.ssh/id_rsa.pub cs15lfa22@ieng6.ucsd.edu:~/.ssh/authorized_keys
# You use your username and the path you saw in the command above*
  
Once you do this, you should be able to ssh or scp from this client to the server without entering your password.
  
Personally, around 5 seconds are saved for me from not using a password.
  
# Part 8: Making Remote Running Even More Pleasant
  
Using everything you've learned, devise the most comfortable method possible for editing WhereAmI.java locally, copying it to the remote server, and running it there.

Few hints-

* To execute a command directly on the remote server, append it to an ssh command with quotes, then log out. For instance, the following command will sign in and display the remote server's home directory:
  
![image](https://user-images.githubusercontent.com/74624958/193384729-9f29f675-d1a2-4299-a0a7-6f0e8d2333f0.png)
  
* You can use semicolons to run multiple commands on the same line in most terminals. For example, try:
  
![image](https://user-images.githubusercontent.com/74624958/193384922-0b6393d2-554e-4688-80bd-9292b9ff9039.png)
  
* You can use the up-arrow on your keyboard to recall the last command that was run
  
## That's it folks!!
## Thank you!!


 
