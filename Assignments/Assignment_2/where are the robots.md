# PicoGym Web Exploitation Writeup


Author: [Sarthak Kohli](https://github.com/SARTHAK811) 

Challenge Page: [where are the robots](https://play.picoctf.org/practice/challenge/4?category=1&page=1)

## Walkthrough
So basically robots.txt file tells the search engine crawlers which file that the creater does not want us to see or may be hide from us.
So when i tried robots.txt(hint given in question and discord server) so it showed me a webpage which showed me Disallow and the location of the page.
It was quite intuitive to check this file and look into it as disallow was written .
So i replaced robots.txt with '/1bb4c.html' which was mentioned in the web page.
Doing that my job was done as it directly gave me the pico flag .
Hence I accessed the files the creator doesn't want me to look:) 
## Flag
`picoCTF{ca1cu1at1ng_Mach1n3s_1bb4c}`

## Useful resources (if any)
Hint given on discord server and Googling robots.txt.
