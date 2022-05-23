Link to [my repository](https://github.com/rhankin214/markdown-parser) <br>
Link to [the repository I reviewed](https://github.com/Aaron3963/MarkdownParser/tree/696feae51b051b26954bcb919366c1c69f51187b)
## Making Markdown Parser handle backticks
Here's the [test file](https://github.com/rhankin214/markdown-parser/blob/main/test-backticks.md) for this one
Using the preview function on that page, we can see the backticks only interfere with the link if it puts the open bracket <br>
Based on that, here's my test implementation: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/BackticksImplementation.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/LinkHelper.png)
<br> And here's both mine and the reviewed repository failing that test (in that order): <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/MyBacktickFailure.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/FeedbackFailsBackticks.png)
<br>
To make this handle backticks correctly you just need the program to skip over open and close brackets in code blocks, something like:
```
int firstBacktick = markdown.indexOf("`", currentIndex);
int secondBacktick = markdown.indexOf("`", firstBacktick);
if(openBracket > firstBacktick && openBracket < secondBacktick)
{
  currentIndex = secondBacktick + 1;
  continue;
}
```
And repeat the same for close bracket, since that also breaks the link if it's in the backticks. The parens being in backticks doesn't cause any problems. <br>

## Making Markdown Parser handle long strings
Here's that [test file](https://github.com/rhankin214/markdown-parser/blob/main/test-long.md) again <br>
So here we can see that any linebreaks stop the link from working, but the text being so long it's more than one line is fine <br>
Here's my test: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/LongImplementation.png) <br>
And here are the failures (same order as before)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/MyLongFailure.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/FeedbackFailsLong.png) <br>
Fixing this is pretty simple. We just need to check if there's a line break anywhere between our indexes
```
int nextLinebreak = markdown.indexOf("\n", openBracket);
if(nextLinebreak != -1 && nextLinebreak < closeParen)
{
  currentIndex = openBracket + 1; 
  continue;
}
```
We set current Index to openBracket + 1 for cases where the bad link just has no close parentheses and using closeParen + 1 might skip over a different valid link. <br>

## Making Markdown Parser handle nested links
The [test file](https://github.com/rhankin214/markdown-parser/blob/main/test-nestedLinks.md) <br>
From this one we can see that having a link in the open bracket invalidates the outer link, the url stops at the parentheses that matches the first, and nested
brackets are fine as long as there's no link. <br>
My test: <br>
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/NestedImplementation.png)
Failures:
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/MyNestedFailure.png)
![Image](https://rhankin214.github.io/cse15l-lab-reports/Lab_4_Screenshots/FeedbackFailsNested.png)
<br>
Honestly, the easiest thing to handle the nested brackets seems like just calling getLinks on the string within the brackets.
```
ArrayList<String> withinBrackets = getLinks(markdown.substring(openBracket, closeBracket));
if(withinBrackets.size() > 0)
{
  for(int i = 0; i < withinBrackets.size; i++)
    toReturn.add(withinBrackets.get(i));
  
  currentIndex = closeBracket + 1;
  continue;
}
```
For the nested parentheses, there was something for that in the updated parser they gave us in Lab period 8, where it just counts parens to make sure they match up.

```
int numOpenBrackets = 1;
int currIndex = openParen;
while(NumOpenBrackets > 0)
{
  if(markdown.indexOf("(", currIndex) > markdown.indexOf(")", currIndex))
  {
    currIndex = markdown.indexOf("(", currIndex) + 1;
    numOpenBrackets++;
  }
  else
  {
    currIndex = markdown.indexOf(")", currIndex) + 1;
    numOpenBrackets--;
  }
}
closeParen = currIndex - 1; //when the loop terminates, currIndex should be one space ahead of the final close paren.
```
That's based on my memory of what the one in lab did but I worked out the details myself. I can only cut that down to 11 lines without ruining my formatting. 
It's so close that I'm sure there's way to go under 10, but I'm stumped as to what it is.
