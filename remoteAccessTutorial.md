# Remote Access Tutorial
In this tutorial i will be teaching you, a new student enrolled in 15l, how to use remote access to connect to computers at the UCSD campus to perform different tasks.

## Installing Visual Studio Code

The very first step you will need to take is to install Visual Studio Code. You will be using Visual Studio Code to make programming files, but mostly for using terminal. In terminal you will run different commands to do different CS15L related stuff.

First click this link: [Visual Studio Link](https://code.visualstudio.com/) 

doing so should take you to Visual Studio Code front page: 
![image](https://user-images.githubusercontent.com/97646229/162661223-7ae49684-4c01-4da3-8554-e67acfa13b56.png)

select the operating system you have currently in use, and click download.
Open the file, complete the setup, and then open the Visual Studio Code application.
Once Visual Studio Code is open it should look like this:
![image](https://user-images.githubusercontent.com/97646229/162661768-42e0ec20-355b-4b9e-84ec-29f1fe50bdc2.png)

## Remote Connecting

**Step 1**, *Install OpenSSH (Windows only)*: if you are not using windows then skip to step 2,

Install OpenSSH: [OpenSSH](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) 

**Step 2**, *Prepare your 15l account*:

look up your course-specific account here: [Account-Lookup](https://sdacs.ucsd.edu/~icc/index.php)
next, fill in your ucsd account information under "Account Lookup".
Once that is completed, you will need to reset your password.
First click this button:
![image](https://user-images.githubusercontent.com/97646229/162663520-8475f428-a48f-4317-b511-831914f8cb1c.png)

your button may contain a few different letters at the end, otherwise it should look the same.
next you will be brought to a page displaying your course-specific account name, be sure to save it somewhere.
Below your account name click the link that says: "Global Password Change Tool"
![image](https://user-images.githubusercontent.com/97646229/162663788-4b6a5131-c9a1-4150-afee-c8fca90db3c3.png)
then fill out the rest of the neccesary information from there. Be sure to remember your new password!

**Step 3**, *connect to a remote server*:

In Visual Studio Code, open terminal.
![image](https://user-images.githubusercontent.com/97646229/162664341-5b356855-66fc-414a-b8d0-5c1f79ee51a5.png)

in terminal type the following command, but be sure to replace "zz" with the ending letters accociated with your course specific account:
`ssh cs15lsp22zz@ieng6.ucsd.edu`

you may be prompted with this text if it is your first time connecting, simply type yes:
`The authenticity of host 'ieng6.ucsd.edu (128.54.70.227)' can't
be established.
RSA key fingerprint is
SHA256:ksruYwhnYH+sySHnHAtLUHngrPEyZTDl/1x99wUQcec.
Are you sure you want to continue connecting
(yes/no/[fingerprint])?`

if all goes according to plan your terminal should look like this:
![image](https://user-images.githubusercontent.com/97646229/162664832-90eeb66b-3a6c-4c5a-abc5-22c5847a4a2a.png)

## Trying Some Commands

all the commands you can use on your local computer in terminal, (the client) can also be used when connected to a server. Try it out!
Here are some examples:

![image](https://user-images.githubusercontent.com/97646229/162666877-3c9acdb2-be5f-47b0-8665-8aeb72930dba.png)

## Moving Files with scp

First create a new java file with the following code:

```
class WhereAmI {
    public static void main(String[] args) {
        System.out.println(System.getProperty("os.name"));
        System.out.println(System.getProperty("user.name"));
        System.out.println(System.getProperty("user.home"));
        System.out.println(System.getProperty("user.dir"));
    }
}
```

compile it using `javac` and run it using `java` on the client.

it should look something like this:

![image](https://user-images.githubusercontent.com/97646229/162668190-1bad1e04-2fe5-4f96-bab1-7d6f1495388d.png)

as you can see it prints information tied to your computers client.

now lets move the file from our client to the server. run this command: 
`scp WhereAmI.java cs15lsp22zz@ieng6.ucsd.edu:~/` (once again, replace zz with your course specific account letters)

now connect to the server by repeating **step 3** in Remote Connecting, and type in the command ls.
![image](https://user-images.githubusercontent.com/97646229/162669022-119eca79-e6b6-4739-ad16-243369fc3acf.png)
as you can see the file has succesfully been moved to the server. If you compile and run the file while connected to the server, you will see it prints information tied to the servers operating system.
![image](https://user-images.githubusercontent.com/97646229/162669199-d45fdfef-8864-4e3f-a574-5e6a7ce5cf55.png)

## Setting an SSH key

Next we will set an SSH key so we do not have to retype a password everytime we use ssh or scp.

run the command `ssh-keygen`
when prompted with wich file to save the key in, type: `/Users/<user-name>/.ssh/id_rsa`

do not set a passphrase, when prompted with setting a passphrase, both times just leave it empty and press enter.

Next connect to the server and make a new directory called .ssh by typing `mkdir .ssh`

now use the scp command to move your `id_rsa.pub` file to the .ssh directory on the server

Congratulations, now you no longer have to type your password everytime you want to use an ssh or scp command.
	
![image](https://user-images.githubusercontent.com/97646229/162673603-c7d51ab9-96a7-4888-baf6-6d1f27341b70.png)


## Optimizing Remote Running

to run a command on the server right upon connection, you can qoutes after the ssh command, for example `ssh cs15lsp22zz@ieng6.ucsd.edu "pwd"` connects to the server, then prints the servers working directory right upon connection.

to run multiple commands on the same line use semicolons between each command. For example: `javac WhereAmI.java; java WhereAmI`

using both of these tips, we can make a local copy of a file, move the file to the server, connect to the server, and then compile and run the file all in one line: 
`cp WhereAmI.java OtherMain.java; scp OtherMain.java cs15lsp22zz@ieng6.ucsd.edu:~/; ssh cs15lsp22zz@ieng6.ucsd.edu "javac OtherMain.java;java WhereAmI"`

![image](https://user-images.githubusercontent.com/97646229/162678921-a31f7560-16c9-49cc-99cc-cbf882a1475c.png)

bonus tip: use the up arrow to autofill your most recently runned command

















