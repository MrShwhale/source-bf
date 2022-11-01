# source-bf
A P'' (also known as brainf) interpreter written in the Source Engine console

## How to install
Simply unzip the release (or download the source code) and place the brainf folder into your cfg folder for your source game of choice.

Then, open the in-game console and run the "exec brainf/brainf" command

Now, you should be able to type the commands into the console window, and they will execute

You can run the sample program with "exec brainf/dee"

## Creating programs
To create a program, make a copy of the program_template.cfg file.

Before the first semicolon on each line, enter the command that you want to run. 

After writing the program

See dee.cfg for a full example of this. 

### Basic commands
Each command corresponds to a brainfuck command. 
Alternate names for the commands were used to avoid conflict with user input.

#### inc
Increases the value of the byte the data pointer is at by 1. 

Overflows to 0 if the byte is 255. Equivalent the '+' command in brainfuck.

#### dec
Decrement the value of the byte the data pointer is at by 1. 

Overflows to 255 if the byte is 0. Equivalent the '-' command in brainfuck.

#### ptr+
Increment the data pointer, making it point to the data cell with a value one higher.

If the current pointer is the last (default: 511), prints an error to console, but does not stop execution. Equivalent the '>' command in brainfuck.

#### ptr-
Decrement the data pointer, making it point to the data cell with a value one lower.

If the current pointer is the first (default: 0), prints an error to console, but does not stop execution. Equivalent the '<' command in brainfuck.

#### out
Outputs a single ASCII character to the console, followed by a newline. 

Unprintable characters (such as ASCII SYN, DEL), white space, as well as the ; and " characters will print an empty line to the console. Trying to print characters with a higher than 127 will print 5 question marks since the engine cannot print them. Equivalent to '.' command in brainfuck.

#### User input
All single characters are commands that set the current bit to the ASCII value of that character.

Has support for any non-whitespace printable character with an ASCII value lower than 128, other than ;, +, - and ". 

### Loop command 
Loop commands are done slightly differently since this is the simplest implementation I have come up with.
Basically, instead of the usual "alias "c<x>" "<command>; airgap; c<x+1>"", loops follow different syntax:

alias "c<x|y>" "alias skip c<y+1>; alias next c<x+1>; test_0"

This line is used in place of both the start and end loop commands, where the start of the loop is at command x and the end is at command y.

For example, a loop that starts on command 12 and ends on command 27 would look like this:
<pre><code>
//c0-11
alias "c12" "alias skip c28; alias next c13; test_0"
//c13-26
alias "c27" "alias skip c28; alias next c13; test_0"
//c28-end
</code></pre>

An example of a loop can be seen in dee.cfg

### Input buffer
There is also support for an input buffer that the user enters characters into prior to execution.

To use the input buffer, make a copy of buffer.cfg and put characters before the first semicolon of a line, like commands when creating a program. To read a byte from the buffer, exec the buffer file at the start of your program, and use the read command to store the next buffer byte in the currently selected byte.

Buffer files can be extended easily (just follow the format), and reading from a full buffer will print an error message in the console, but will not stop execution.
