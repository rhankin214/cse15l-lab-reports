## Lab report 5: comparing implementations
In this lab I compared my implmentation with another one using vimdiff. Here's some test files they differed on.
### Test file 1: [193.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/193.md) <br>
Screenshot of vim diff and results: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_5_Screenshots/Second_diff.png) <br>
Left one is mine, right one is given implementation <br>
We can tell from the github preview that the link is functional and leads to a page called "url." In this case, my implementation is correct.
The given implementation can't handle cases where the link is in this alternate link format with no parens.

according to github preview
describe bug in code in 2-3 sentences with screenshot.

### Test file 2: [503.md](https://github.com/nidhidhamnani/markdown-parser/blob/main/test-files/503.md)<br>
Screenshot of vim diff and results: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_5_Screenshots/Second_diff.png) <br>
From the preview it's just supposed to add "title", but with my implementation it doesn't add the link, and with the left one it adds a bunch of random stuff it's not supposed to. With mine it seems it can't handle a url in quotes, and with the given it seems to break and add the wrong info when it gets a url in quotes.
