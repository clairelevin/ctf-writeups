# Bbbbloat (picoCTF 2022)

When run, this program prints “What’s my favorite number?”

![](/ctf_screenshots/bloat_1.png)
 
Looking at the program in Binary Ninja, it appears that the user input is compared to the value 549255.

![](/ctf_screenshots/bloat_2.png)
 
When 549255 is entered after the “What’s my favorite number?” prompt, the flag is printed.

![](/ctf_screenshots/bloat_3.png)
