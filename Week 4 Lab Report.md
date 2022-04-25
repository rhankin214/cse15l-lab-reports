## Markdown Parser Bug Squashing
### Bug 1: Treating image as link
<br> One problem with the markdown parser is that it treats images as links. With [test-file6](https://github.com/rhankin214/markdown-parser/blob/main/test-file6.md), there's an image marked by a "!". The bug is that our markdown parser doesn't make note of the exclamation point. The symptom is that since the parser can't tell its an image. the image winds up in the arraylist of links, as you can see here: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Image_catching_output.png)<br>
We can fix this by having the parser check if there's an exclamation point just before the open bracket. I added this code to getLinks to do that : <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Image_catching_changes.png) <br>

The try-catch block is in case the bracket is the very first character. If the index before OpenBracket is -1, there's definitely not an exclamation point there so we can run as normal.<br><br>

### Bug 2: Not acknowledging space between parens and brackets
<br> Another bug arises with [test-file5](https://github.com/rhankin214/markdown-parser/blob/main/test-file5.md). Links in markdown don't work properly unless the '[the bracket part]' and '(TheUrlPart)' are right next to each other. The symptom is that even though there's multiple characters between the two parts and the link doesn't work, the parser still adds it to the output: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Space_between_output.png)<br>
We can fix this by simply putting an if statement that checks that openParen is exactly one more than closeBracket.
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Space_between_changes.png) <br><br>

### Bug 3: Cannot handle index = -1
<br> The final bug we're going to talk about involves [test-file3](https://github.com/rhankin214/markdown-parser/blob/main/test-file3.md). In the initial version of the parser, running test file 3 would give the following output:<br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Bracket_without_paren_output.png)
<br> The bug is that the parser still tries to add a substring even if it gets -1 for the index of the parentheses. The exception is a symptom of that bug. We can fix this by just breaking the loop if any of the indexes return -1, like so:
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Bracket_without_paren_changes.png)
<br> This fixes some other failure inducing inputs too, like an infinite loop with [test-file2](https://github.com/rhankin214/markdown-parser/blob/main/test-file2.md) where current index keeps getting set back to zero because the index of closeBracket keeps going to -1. You could consider that another symptom of the same bug.
