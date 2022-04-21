# Dragon Pit (UMDCTF 2022)

This binary requires a higher version of glibc than I had, so I was not able to run it. Rather than install a new version of glibc, I solved this challenge by analyzing the code in Ghidra without running it.
 	
  ![](/ctf_screenshots/dragonpit_1.png)
 
The program prints out “When should Fred jump into the dragon pit?” If the correct string is entered in response, the program prints out the flag.

 ![](/ctf_screenshots/dragonpit_ghidra.png)
 
It appears that the flag is constructed on the stack. Each section of the flag string is labeled below.

![](/ctf_screenshots/dragonpit_labeled.PNG)
 
After reassembling the flag string in the correct order, we obtain `UMDCTF{BluSt0l3dr4g}`.
