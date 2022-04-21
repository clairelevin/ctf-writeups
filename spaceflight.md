# Spaceflight (Space Heroes CTF 2022)

This challenge has several stages. The first stage prompts us to enter a launch password.
 
 ![](/ctf_screenshots/spaceflight_1.png)
 
The string “b3y0nd!infinity” is stored in memory under the variable name “launch_password.” After entering this string at the prompt, we can now move on to the next phase.
 
  ![](/ctf_screenshots/spaceflight_2.png)
 
The next phase tells us that we have 0.1 seconds to respond to the next prompt. 
 
  ![](/ctf_screenshots/spaceflight_3.png)
 
However, a look at the disassembly reveals that there is not actually a timer running, and the program is instead checking whether the variable “timer_cancelled” was ever set to 1. This variable is set in the function “cntrl_c_handler,” so we need to generate a signal to trigger a call to the handler.
 
  ![](/ctf_screenshots/spaceflight_4.png)
 
The signal 2 corresponds to the signal `SIGINT`, which we can trigger by entering `Ctrl+C`. Once the handler is triggered, we get a message telling us the “explode timer” is suspended.
 
  ![](/ctf_screenshots/spaceflight_5.png)
 
At this point, a function called “check_jettison” is called. There is a call to sscanf with the format specifier “%d %d %d %d,” indicating that we need to enter a sequence of four digits.
 
  ![](/ctf_screenshots/spaceflight_6.png)
 
Looking at the code that checks our user input, two things are immediately clear: each of the digits we have entered needs to be between 0 and 3, and our input is at some point compared to a variable called “jettison_sequence.” It turns out that “jettison_sequence” is an array of four integers: 2, 3, 0, 1.
 
  ![](/ctf_screenshots/spaceflight_7.png)
 
Even without knowing exactly what the “check_jettison” function is doing, we can guess that “2 3 0 1” is probably the right input. This proves to be correct, and we can move on to the next phase.
 
  ![](/ctf_screenshots/spaceflight_8.png)
 
We can see that we need to enter 3 numbers – otherwise we will get an error message of “NOT ENOUGH NUMBERS!”

 ![](/ctf_screenshots/spaceflight_9.png)

Each of the three numbers needs to be positive to avoid the error message “NEGATIVE!” , but their sum needs to overflow so that the result is exactly -1 (otherwise we will get an error of “NOT NEGATIVE ENOUGH!”) .
 
  ![](/ctf_screenshots/spaceflight_10.png)
 
We can enter any three numbers that satisfy these criteria (2147483647 2147483647 1 is one such sequence) to move on to the next phase:
 
  ![](/ctf_screenshots/spaceflight_11.png)
 
Binary Ninja’s decompiler fails to analyze the function corresponding to this phase – it incorrectly suggests that the function never returns. This means we need to look at the disassembly to determine how our input is being checked.
 
  ![](/ctf_screenshots/spaceflight_12.png)
 
The value at rbp-0x1 is compared to the character “\*”, and the value at rbp-0x5 is compared to the string “jump.” Putting these together, we find that the correct input is “jump*”. 
Once we enter this input, the flag is printed:
`shctf{Th3-expl0Ration-oF-Spac3-wi11-go-ah3ad}`
