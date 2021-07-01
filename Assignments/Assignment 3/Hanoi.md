# Micro Corruption Embedded Security CTF Writeup


Author: [Sarthak Kohli](https://github.com/SARTHAK811) 

Challenge Page: [Hanoi](https://microcorruption.com/cpu/debugger)

## Walkthrough
Step 1:
I entered 'c' command and tried the password '1234567891011' and again enetered 'c' command.
Ofcourse the password did not work for me so i analyzed the login function
4520 <login>
4520:  c243 1024      mov.b	#0x0, &0x2410
4524:  3f40 7e44      mov	#0x447e "Enter the password to continue.", r15
4528:  b012 de45      call	#0x45de <puts>
452c:  3f40 9e44      mov	#0x449e "Remember: passwords are between 8 and 16 characters.", r15
4530:  b012 de45      call	#0x45de <puts>
4534:  3e40 1c00      mov	#0x1c, r14
4538:  3f40 0024      mov	#0x2400, r15
453c:  b012 ce45      call	#0x45ce <getsn>
4540:  3f40 0024      mov	#0x2400, r15
4544:  b012 5444      call	#0x4454 <test_password_valid>
4548:  0f93           tst	r15
454a:  0324           jz	$+0x8
454c:  f240 6500 1024 mov.b	#0x65, &0x2410
4552:  3f40 d344      mov	#0x44d3 "Testing if password is valid.", r15
4556:  b012 de45      call	#0x45de <puts>
455a:  f290 fe00 1024 cmp.b	#0xfe, &0x2410
4560:  0720           jne	#0x4570 <login+0x50>
4562:  3f40 f144      mov	#0x44f1 "Access granted.", r15
4566:  b012 de45      call	#0x45de <puts>
456a:  b012 4844      call	#0x4448 <unlock_door>
456e:  3041           ret
4570:  3f40 0145      mov	#0x4501 "That password is not correct.", r15
4574:  b012 de45      call	#0x45de <puts>
4578:  3041           ret

i put a breakpoint at test password _valid function but it turned out to be of no use after doing the analysis of the function .
Moving further i see the command cmp.b which compares bitwise and if that comparison is true  then we will not jump as the comparison gives zero and jne fails and hence
we will got to "Access granted" line .
Having said that I noticed that 0X2410 is 16 bytes away from the initial character so basically the checking is only done at  17th character so 
putting any random 16 characters and then 17 should be fe in hexa and we are done.
I entered solve command to finish the problem.


## Password
['45454545454545454545454545454545fe](in hexa)

## Useful resources (if any)
1.Tutorial
2.Assembly cheat sheet(https://www.cs.tufts.edu/comp/40/docs/x64_cheatsheet.pdf)
3.Endianness-Wikipedia(https://en.wikipedia.org/wiki/Endianness)