# source-bf
A Brainfuck interpreter written in the Source Engine console

## How to install
Simply place the brainf.cfg file into your cfg folder for your source game of choice.

Then, open the in-game console and run the "exec brainf" command

Now, you should be able to type the commands into the console window, and they will execute

## Creating programs
To create a program, make a copy of the program_template.cfg file.

Before the first semicolon on each line, enter the command that you want to run. 

After writing the program

See dee.cfg for a full example of this. 

### Commands
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

###  Loop command
