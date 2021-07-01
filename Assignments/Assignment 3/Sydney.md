# Micro Corruption Embedded Security CTF Writeup


Author: [Sarthak Kohli](https://github.com/SARTHAK811) 

Challenge Page: [Sydney](https://microcorruption.com/cpu/debugger)

## Walkthrough
Step1:
To start the problem i entered 'c' command and entered a random password say 'test' and again entered 'c' to see what happens.
Ofcourse the password did not work and my program execution stopped due to which i had to enter 'reset' coomand.
Step 2: Analyzing the main function-
The flow in the main function:-
A)Get password function
B)check password function
C)testing for value of r15 and then proceeding.Clearly as per the flow ,it is visible that if value that r15 is storing is 0000 then we will go to Invalid password step and our execution will finally stop.So our aim is that r15 value should not be equal to zero.
For this we will use break points at check password and may be get password functions.
Step 3:Analyzing check password function-
Also if we see the value of r15 after get password function we will notice that r15 is the location from where our password starts that is it is from r15 that we start storing 'test' in this case.
A) In the first step it compares #0X7a38 with 0X0(r15).
The meaning of this comparison is that the first element of r15(considering it as to be an array) should be equal to 7a ,the secnd element should be equal to 38.
We will not jump as the comparison would be equal to zero.
In the next step it comapres 0X7547 with 0X2(r 15).
so the third element should be 75 and the fourth element should be 47.
Following the similar analysis we get the password in hexa as 7a 38 75 47 36 29 28 73.
This will give me r15 as 0001 and not 0000 which i required to crack this problem.
But still this did not work for me so i had to analyze and search more.
I searched net that how sequence of bytes are stored which lead to me a new concept called as Endianness.By trial and testing method i got to know that my password is in little endian form so the final password will be 38 7a 47 75 29 36 73 28(in hexa).
Entering this password solves the lock for me and then i type 'solve' command to finish the problem.

## Password
[38 7a 47 75 29 36 73 28](hexa)

## Useful resources (if any)
1.Tutorial
2.Assembly cheat sheet(https://www.cs.tufts.edu/comp/40/docs/x64_cheatsheet.pdf)
3.Endianness-Wikipedia(https://en.wikipedia.org/wiki/Endianness)