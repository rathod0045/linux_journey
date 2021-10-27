Text-Fu


# Text-Fu

### 1. stdout ( Standard Out )
> $ echo Hello World > peanuts.txt

- $ echo Hello World 
- We know this prints out Hello World to the screen, but how? Processes use I/O streams to receive input and return output. By default the echo command takes the input (standard input or stdin) from the keyboard and returns the output (standard output or stdout) to the screen. So that's why when you type echo Hello World in your shell, you get Hello World on the screen. However, I/O redirection allows us to change this default behavior giving us greater file flexibility. 
- The *>* is a redirection operator that allows us the change where standard output goes. It allows us to send the output of echo Hello World to a file instead of the screen.<br>

> $ echo Hello World >> peanuts.txt 

- (**>>**) This will append Hello World to the end of the peanuts.txt file, if the file doesn't already exist it will create it for us like it did with the > redirector! 

### 2. stdin ( Standard In )

> $ cat < peanuts.txt > banana.txt 

- Just like we had > for stdout redirection, we can use '<' for stdin redirection. Normally in the cat command, you send a file to it and that file becomes the stdin, in this case, we redirected peanuts.txt to be our stdin. Then the output of cat peanuts.txt which would be Hello World gets redirected to another file called banana.txt.

### 3. stderr ( Standard Error )

> $ ls /fake/directory > peanuts.txt  <br>
> ls: cannot access /fake/directory: No such file or directory <br>

- By default, stderr sends its output to the screen as well, it's a completely different stream than stdout. So you'll need to redirect its output a different way. 
- We will have to use file descriptors. A file descriptor is a non-negative number that is used to access a file or stream. the file descriptor for stdin, stdout and stderr is 0, 1, and 2 respectively. 
<br>
> $ ls /fake/directory 2> peanuts.txt

- if we want to redirect our stderr to the file we can do this and You should see just the stderr messages in peanuts.txt.  <br>

> $ ls /fake/directory > peanuts.txt 2>&1

- if we wanted to see both stderr and stdout in the peanuts.txt file.
- This sends the results of ls /fake/directory to the peanuts.txt file and then it redirects stderr to the stdout via 2>&1. The order of operations here matters, 2>&1 sends stderr to whatever stdout is pointing to. In this case stdout is pointing to a file, so 2>&1 also sends stderr to a file.<br>

> $ ls /fake/directory &> peanuts.txt

- This is a shorter way to redirect both stdout and stderr to a file.

### 4. pipe and tee
> $ ls -la /etc | less 

- The pipe operator |, represented by a vertical bar, allows us to get the stdout of a command and make that the stdin to another process. 
- In this case, we took the stdout of ls -la /etc and then piped it to the less command. The pipe command is extremely useful and we will continue to use it for all eternity. <br>

> $ ls | tee peanuts.txt banan.txt

- **This command will only display content on screen and write in document you cant use less with this command.**

### 5. env ( Environment )
> $ echo $HOME

- You should see the path to your home directory.<br>

> $ echo $USER 

- You should see your username!<br>

**$ env**

- **This will display all the Environment variable.**<br>

> $ echo $PATH <br>
/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin

- This returns a list of paths separated by a colon that your system searches when it runs a command. 

### 6. cut
We're gonna learn a couple of useful commands that you can use to process text. <br>
example = 'The quick brown; fox jumps over the lazy  (tab) dog' <br>
> $ cut -c 5 sample.txt

- This outputs the 5th character in each line of the file. In this case it is "q", note that the space also counts as a character. <br>

> $ cut -f 2 sample.txt

- The -f or field flag cuts text based off of fields, by default it uses TABs as delimiters, so everything separated by a TAB is considered a field. You should see "dog" as your output.<br>

> $ cut -f 1 -d ";" sample.txt

- This will change the TAB delimiter to a ";"
-  **N   N'th byte, character or field, counted from 1**
-  **N-   from N'th byte, character or field, to end of line.**
- **N-M   from N'th to M'th (included) byte, character or field**
-  **-M    from first to M'th (included) byte, character or field**

### 7. paste
The paste command is similar to the cat command, it merges lines together in a file.<br>
> $ paste -s sample2.txt

- The default delimiter for paste is TAB, so now there is one line with TABs separating each word.

- Let's change this delimiter (-d) to something a little more readable: <br>

> $ paste -d ' ' -s sample2.txt

- Now everything should be on one line delimited by spaces. 

### 8. head

- if you just wanted to see the first couple of lines in this text file, you can do that with the head command, by **default the head command will show you the first 10 lines in a file.**<br>

> $ head /var/log/syslog

- You can also modify the line count to whatever you choose, let's say you wanted to see the first 15 lines instead.<br>

> $ head -n 15 /var/log/syslog

- The -n flag stands for number of lines. 

### 9. tail
- Similar to the head command, the tail command lets you see the last 10 lines of a file by default.<br>

> $ tail /var/log/syslog

- Another great option you can use is the **-f (follow) flag**, this will follow the file as it grows. <br>

> $ tail -f /var/log/syslog

- Your syslog file will be continually changing while you interact with your system and using tail -f you can see everything that is getting added to that file.

### 10. expand and unexpand

- Normally TABs would usually show a noticeable difference but some text files don't show that well enough. Having TABs in a text file may not be the desired spacing you want. To change your TABs to spaces, use the expand command. <br>

> $ expand sample.txt

- The command above will print output with each TAB converted into a group of spaces. To save this output in a file, use output redirection like below.
<br>

> $ expand sample.txt > result.txt

- Opposite to expand, we can convert back each group of spaces to a TAB with the unexpand command: <br>

> $ unexpand -a result.txt (a for all blanks )

### 11. sort
- content of file1.txt <br>
> dog
> cow
> cat
> elephant
> bird

$ sort file1.txt<br>
> bird
> cat
> cow
> dog
> elephant

- **-r reverse sort.**
- **-n numerical sort.**

### 12. tr ( Translate )

- The tr (translate) command allows you to translate a set of characters into another set of characters. Let's try an example of translating all lower case characters to uppercase characters.<br>

> $ tr a-z A-Z <br>
> hello<br>
> HELLO<br>

- As you can see we made the ranges of a-z into A-Z and all text we type that is lowercase gets uppercased. 

### 13. wc (word count) and nl (number lines)
- The wc (word count) command shows the total count of words in a file.<br>

> $ wc /etc/passwd <br>
>96     265    5925 /etc/passwd

It display the **number of lines ( -l ) : number of words ( -w ) : number of bytes  ( -c )** respectively.

- Another command you can use to check the count of lines on a file is the nl (number lines) command.<br>

file1.txt<br>
>i<br>
>like<br>
>turtles<br>

> $ nl file1.txt

>1. i 
>2. like
>3. turtles

### 14. grep
 - The grep command is quite possibly the most common text processing command you will use. It allows you to search files for characters that match a certain pattern. What if you wanted to know if a file existed in a certain directory or if you wanted to see if a string was found in a file? You certainly wouldn't dig through every line of text, you would use grep!

- Let's use our sample.txt file as an example:<br>

> $ grep fox sample.txt

- You should see that grep found fox in the sample.txt file.

- You can also grep patterns that are case insensitive with the -i flag:<br>

> $ grep -i somepattern somefile

- To get even more flexible with grep you can combine it with other commands with |.<br>

> $ env | grep -i User

- As you can see grep is pretty versatile. You can even use regular expressions in your pattern:

> $ ls /somedir | grep '.txt$' <br>

- Should return all files ending with .txt in somedir. 
