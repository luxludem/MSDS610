# MSDS610
This repository will show you how to efficiently use the terminal to quickly summarize data without having to write a python script or open Jupyter Notebook.
### Introduction
As data scientists, we spend a lot of time trying to understand and work with data.  We need quick ways to preview data or make it easier to work with, and this is where streams come in handy.  Streams are input and output connections between a program and its environment.  Redirection refers to how a stream is controlled.  A stream can be redirected to achieve different results.  Using streams and redirection is a way to combine commands together to make more  powerful commands so data can be quickly analyzed.  
This repository will discuss the three main components of streams:  Standard Input, Standard Output, and Standard Error.  Then, it will summarize these concepts through an example.  
### Standard Input
Standard input stream carries data from a user to a program.  When standard input stream is not redirected, it will read input from the terminal.  
To redirect standard input, use the '<' symbol.  The example below redirects the input to the cat command to use the text file 'foo.txt' instead of standard input.  
EX:  <code>$ cat \< foo.txt</code>
### Standard Output
Standard output writes data generated by a program or a command. When the standard output stream is not redirected, it will output text to the terminal.
To redirect standard output, use the '>' symbol. The example below redirects the output of ls to a file 'bar.txt' instead of the default output in the terminal.
EX:  <code>$ ls > bar.txt</code>
## Frequently used commands
Now, we are going to introduce a few common terminal commands and show some examples to get started using streams and I/O redirection.  
    
Let's start with a basic word count command, which will count the words of the input.
<pre><code>$ wc output.csv</code></pre>
Next, we can add in a pipe, represented with a '|'.  The | symbol is used to pass the standard output of one program to the standard input of another program.  
<pre><code>$ grep 'sales' output.csv | wc</code></pre> 
What if we want to save the result of the command to a file?  Use redirection!  
<pre><code>$ grep 'sales' output.csv | wc > result.txt </code></pre>  
### Standard Error
Standard error is where errors are written that are generated by a failed program.  Similar to standard output, the default output for standard error is the terminal.  
<pre><code>$ pdftotext test.txt > greatness.txt </code></pre> 
![Error1](Error1.png)
    
These errors are part of the third continuous stream. The error encountered isn’t pushed through the output stream but the error stream and outputted to the terminal as shown above. There are only 29 possible command line errors when you don’t import libraries. 
### Streams and Redirection with csvkit
To combine some of the items discussed above, I will walk through a longer example of using a stream with csvkit.  
To install and get started with csvkit, which is a program that can be used to process csv files using UNIX commands, use brew install.  
<pre><code>$ brew install csvkit</code></pre>  
Now, on to the example:
<pre><code>csvcut -c 3 -e latin1 file.csv | tail +2 | sort | uniq -c | sort -r -n | head -5 > out.txt</code></pre> 
Here are the steps to walk through this long command stream:  
1.  There are 3 starting arguments passed into the csvcut command.  
    -  -c 3: tells csvcut to look at 3rd column of csv file
    - -e latin1: tells csvcut to use ‘latin 1’ encoding
    - file.csv:  is the input csv file
2.  The output of #1 is then piped into the tail command; 'tail +2' tells the program to start at the 2nd row of the file and go to the end
3.  The output of #2 is then piped into the sort command; the results are sorted in ascending order by default.
4.  The output of #3 is then piped into the unique command; 'unique -c' eliminates duplicates and returns unique results with a count added.  (Note, the -c is the argument to add the count.)
5.  The output of #4 is then piped into another sort command.  This time 'sort -r -n' includes arguments to sort in reverse order by number.  In this case the sorting will be based on the count added in the previous step with the 'unique -c' command.
6.  The output of #5 is then piped into the head command to get the top 5 results.
7.  The final step redirects the output to a txt file to save for easy reference later.

    


