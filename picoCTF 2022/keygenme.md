# Keygenme (picoCTF 2022)
This challenge asks us to reverse-engineer a binary called “keygenme.” When run, it prompts us for a license key.

![](/ctf_screenshots/keygenme_enter_key.png)
 
The main function of the binary is shown below. It appears that the program passes the user input to some function, then prints either `“That key is invalid.”` or `“That key is valid.”`
 
![](/ctf_screenshots/keygenme_binja_1.png)
 
Looking at sub_1209, it appears that the flag starts with “picoCTF{br1ng_y0ur_0wn_k3y_}”. The remaining characters of the flag seem to be generated via repeated calls to the MD5 function.
 
 ![](/ctf_screenshots/keygenme_binja_2.png)
 
Once the flag is generated, the subroutine returns either success or failure depending on whether the user input is equal to the completed flag. 

![](/ctf_screenshots/keygenme_binja_3.png)
 
Since the complete flag must be stored on the stack in order for this comparison to occur, I ran the program in GDB and set a breakpoint right before the subroutine returned. I then checked the contents of the stack and found the flag there.
 
 ![](/ctf_screenshots/keygenme_flag.png)
 
`picoCTF{br1ng_y0ur_0wn_k3y_d6f78070}` was the correct flag.
