### CSE 15L Lab Report 1: How to set up SSH
## Step 1: Setting up VS code
![Image](https://logowik.com/content/uploads/images/visual-studio-code7642.jpg)
<br>
Setting up VS code is easy. Just follow [this link](https://code.visualstudio.com/download) and pick the version for your machine. Once the installer is downloaded,
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
## Step 5: Moving files with SCP
The server's not worth much to us if we can't run our own programs on it. To do that we use `scp` to send files we write on our own computers over to the server.
The format for an scp command is simply 'scp <filename> cs15lsp22aaa@ieng6.ucsd.edu:~/'. Remember to replace 'aaa' with your unique letter combination.
<br>
You can also send it to a specific directory in the server by putting `cs15lsp22aaa@ieng6.ucsd.edu:~` and insert the filepath after the '~'
Here's an example of me using scp to move the example.txt file from my own pc to the server.
![Image](https://rhankin214.github.io/cse15l-lab-reports/scp_example_1.png)
<br>As you can see, it's now in the main directory of the server. If it was a java file, I could now compile and run it with the javac and java commands.
<br> <br>
## Step 6: Speeding things up with keys
The way we just did that _worked_, but it was very inefficient. To run a java file on the server that way, we have to
1. run scp command
2. enter password
3. run ssh command
4. enter password
5. javac to compile
6. java to run
Doing that over and over for an assignment would take a long time, so lets start by cutting out the password step. We can use `ssh-keygen` generate a key that will let the server recognize our computer so we don't have to enter our password every time. 
<br>
Here are the steps to setting up and sending an ssh key <br>
1. run the 'ssh-keygen' command. If you're on windows you may need to use 'ssh-keygen -t ed25519' instead, although I could just use 'ssh-keygen' when I tried it myself just now <br>
2. You will be prompted for which file to save the key it. If you just press enter without typing it will use the defalut file path in parentheses. In my experience it's easiest just to use the default. <br>
3. Login to the server using ssh and use the 'mkdir' command to make a directory title .ssh. Then log off. <br>
4. Then use scp to send your key. If you're not sure where it is, you can scroll up in the terminal to where you entered (or used the default) file path. You can navigate to the correct directory using 'cd' or use an scp command that specifies the file path in the format. There will be two keys in the directory, and one of their names will end in .pub. That's the one you want to send. For the scp command add ':~/.ssh/authorized_keys' after the server address to copy the key into the right file. <br>
5. Enter your password for hopefully the last time. Now running files on the server will be much more efficient.

Here's some screen shots depicting the whole process <br>

![Image](https://rhankin214.github.io/cse15l-lab-reports/keygen_example_1.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/keygen_example_2.png)
`cd`

## Step 7: further optimization
We've cutout the passwords, but running a file on the server still takes multiple commands. We have two techniques we can use to make multiple commands into one. 
1. We can use ";" to separate two commands, which the computer will run one after the other
2. We can put "" after the ssh command to specify commands we want to run on the server. Doing this also saves us the trouble of logging out of hit.
By combining these techniques, we can make the command: <br> <br>
scp filename.java cs15lsp22aaa@ieng6.ucsd.edu:~/; ssh cs15lsp22aaa@ieng6.ucsd.edu "javac filename.java; java filename" <br> <br>
This command sends the newest copy of a file to the server and runs it there, and each time we want to run it again we just have to press the up arrow and enter, which only takes seconds. Here's a screenshot showing it in action with a file called printerMan that simply announces  thatit works. <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/printerManScreenshot.png)
