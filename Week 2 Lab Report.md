### CSE 15L Lab Report 1: How to set up SSH
## Step 1: Setting up VS code
![Image](https://logowik.com/content/uploads/images/visual-studio-code7642.jpg)
<br>
Setting up VS code is easy. Just follow [this link] (https://code.visualstudio.com/download) and pick the version for your machine. Once the installer is downloaded,
run it and follow the instructions. <br>
When you open vs code, you should see this screen:
![Image](https://rhankin214.github.io/cse15l-lab-reports/vsc%20mainscreen.png)
<br><br>

## Step 2: Set your ssh password.
You might not need to do this bit. If you haven't used ssh in a previous class, you'll very likely need to change your password 
[here](https://sdacs.ucsd.edu/~icc/password.php) due to not having any password set for the class.
![Image](https://rhankin214.github.io/cse15l-lab-reports/Global%20password%20reset.png)
When you set the password, make sure the drop down circled in blue is set to yes.
Make note of the text circled in red. That's part of the address of the server you'll use. 
<br> <br>
## Step 3: connect to a server remotely with SSH
Open vs code and click Terminal -> New Terminal then just enter into the terminal
`ssh cs15lsp22aaa@ieng6.ucsd.edu` but make sure to replace aaa with whatever combination of letters is there on your global password reset page. You'll be prompted for your password. Once you enter it, you should get the following output:
<br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/ssh_output_1.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/ssh_output_2.png)
<br>You're now connected to the server, and any UNIX commands you run will be run on the server rather than your pc. You can use the `exit` command at any time to log off the server.
<br> <br>
## Step 4: Trying some commands
Play around in the server with UNIX commands. Here's a list of commands you can try
- `ls` prints the files and directories in the currnet directory 
- `ls -a` same as above but prints a wider range of things such as .ssh and .config directories
- `cd` moves to the listed directory in the current file, or to the parent directory if none is specified.
- `mkdir <name>` creates a new directory in the current one of the specified name
- `touch <name>` creates a file of the specified name.
<br> Here's some sample output of the ls, mkdir, and touch commands:
![Image](https://rhankin214.github.io/cse15l-lab-reports/unix_command_examples.png)
<br> <br>
