# Introduction to Linux

The first release of the Linux operating system was in 1991 by Linus Torvalds. Since then, it has evolved into one of the most popular and widely used open-source operating systems in the world.

Here are some fundamental Linux commands that you can start using in the terminal to navigate and manipulate your system.

# Common Linux Commands

whoami
Displays the username of the currently logged-in user.

echo
Used to display text or variables.
echo "Hello, Linux!"

ls
Lists files and directories in the current directory.

cat
Displays the contents of a file in the terminal.
cat filename.txt

pwd
Prints the current working directory (the directory you're in).

find
Search for files and directories based on conditions.
find /path/to/search -name "filename"

grep
Searches for a specific pattern in files and outputs the results.
grep "pattern" filename.txt


# Redirection and Operators
In Linux, you can manipulate the flow of input and output using operators. Below are some essential operators:

& (Background Operator)
Runs a command in the background, freeing up the terminal for other tasks.

&& (AND Operator)
Runs the second command only if the first command is successful.
command1 && command2

> (Output Redirection)
Redirects the output of a command to a file, overwriting the file if it exists.
echo "Some text" > output.txt


>> (Append Output)
Redirects the output of a command to a file, but appends it to the end rather than overwriting.
echo "More text" >> output.txt


# Conclusion
These commands and operators are just the basics, but they will form the foundation for your journey into Linux. As you progress, you can start exploring more advanced commands, scripts, and automation tasks.