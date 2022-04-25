## Markdown Parser Bug Squashing
### Bug 1: Treating image as link
<br> One problem with the markdown parser is that it treats images as links. With [test-file6](https://github.com/rhankin214/markdown-parser/blob/main/test-file6.md), there's an image marked by a "!". The bug is that our markdown parser doesn't make note of the exclamation point. The symptom is that since the parser can't tell its an image. the image winds up in the arraylist of links, as you can see here: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Image_catching_output.png)<br>
We can fix this by having the parser check if there's an exclamation point just before the open bracket. I added this code to getLinks to do that : <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_2_Screenshots/Image_catching_changes.png) <br>

The try-catch block is in case the bracket is the very first character. If the index before OpenBracket is -1, there's definitely not an exclamation point there so we can run as normal.<br><br>

### Bug 2: Not acknowledging space between parens and brackets
