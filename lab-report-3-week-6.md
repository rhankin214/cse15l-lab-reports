## Step 1: making a config file

<br> ![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/ssh_improved_config.png) <br>
I made my config file in visual studio code. Being the super creative person I am, I used the same alias as the lab writeup. <br>
This makes the ssh and scp commands much simpler <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/ssh_improved_login.png) <br>
(this one's in command prompt because it's the first one I did and I hadn't opened everything else yet)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/ssh_improved_scp.png)
<br> <br>

## Step 2: Pushing to github with an ssh key

<br> I used keygen to make a key pair on the ssh server and copied the public one to github. Here they are: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/github-key-location.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/key_user_account_location.png)
<br> Doing this lets me push to github from the ssh server. Here's screenshots of that. <br> ![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/commit_in_ssh.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/pushing_from_ssh.png)
<br>
Here's a link to that [commit](https://github.com/rhankin214/markdown-parser/commit/31834092935073ec0c9fb13193f029621505e326)
<br> <br>
## Step 3: Copying directories with scp -r
<br> We can use scp -r to copy the entire markdown parser directory like so: <br> ![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/markdown_parser_scp.png) <br>
Then we can run the tests on the ssh server: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/running_tests_on_ssh.png)
<br>
We can combine these into one command using semicolons and quotes like we did in lab 1. Or, we should be able to, but it causes an error because the compiler tries to run it on a different version of java. I'm not sure how to fix this. <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/Big_command.png)
<br> Leads to: <br> 
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_3_Screenshots/unsupported.png)
<br> Maybe there's a different version of the java and javac commands that specify which version to run, or maybe I could do something with shell scripting?
