# Micro Corruption Embedded Security CTF Writeup


Author: [Sarthak Kohli](https://github.com/SARTHAK811) 

Challenge Page: [New Orleans](https://microcorruption.com/cpu/debugger)

## Walkthrough
Step 1: I enter 'c' then i enter random password say 'test' and then i again enter 'c'
Ofcourse this did not work and program execution stopped.
Step 2: To analyze the password i looked into the main function where i could put a breakpoint and get the password.So i put a breakpoint on the check password function.
Analyzing the check password function:-
1.In check password function, the following flow happens starting from r 14  to be zero it checks r 13 and the memory data starting from 0x2400 bit wise as cmp.b is used which means comparing bitwise.After one comparison it increments the value of r14 by 1. But there is also one more check that r14 should be less than 8 so basically there should be only 8 iterations of the above mentioned type.
which implies that the password is 8 byte long.Since the last charcter is end of file so basically 7 ASCII characters starting from 0x2400.
If this happens then r15 would be 0001 and not 0000 and the function will jump to Access granted step in the main function.

After doing it on the test lock we just type "solve" command to complete the level.

## Password
[g![:b=,]

## Useful resources (if any)
1.Tutorial
2.Assembly cheat sheet(https://www.cs.tufts.edu/comp/40/docs/x64_cheatsheet.pdf)