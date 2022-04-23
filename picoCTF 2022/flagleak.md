# flag leak (picoCTF 2022)

This challenge asks us to obtain the flag by exploiting a program with the following vulnerable function:

![](/ctf_screenshots/flagleak_1.png)
 
The function takes in our input, then calls printf to echo the same string back to us. However, no format specifier is given in the call to printf(story), meaning that we can insert our own format specifiers. If more format specifiers are given than actual arguments, then printf will interpret the next values on the stack as arguments, allowing us to print out the values stored on the stack.
 
![](/ctf_screenshots/flagleak_2.png)
 
Looking at this output, we can see the following sequence of values that appear to be ASCII values:

`0x6f6369700x7b4654430x6b34334c0x5f676e310x67346c460x6666305f0x3474535f0x345f6b630x653531330x7d666631`

Sure enough, this is the flag: `picoCTF{L34k1ng_FL4g_0ff_St4ck_4315e1ff}`.
