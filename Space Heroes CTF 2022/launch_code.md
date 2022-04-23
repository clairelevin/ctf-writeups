# Launch Code (Space Heroes CTF 2022)
We are given a program that prints the following:

![](/ctf_screenshots/launchcode_1.png)
 
We need to enter the correct code before 30 seconds are up. Looking at the program in Binary Ninja reveals that this launch code takes the form of four hexadecimal digits separated by spaces.
 
 ![](/ctf_screenshots/launchcode_2.png)
 
There are three functions called “three,” “two,” and “one” that check the input. This allows us to generate a launch code in the correct format. In the screenshot below, nonce is a random nonce printed out at the start of the program, and code_1 through code_4 are the four hexadecimal digits of the user input in the order they are entered.
 
 ![](/ctf_screenshots/launchcode_3.png)
 
This reveals that the following conditions must hold:
-	(nonce + code_1 + code_2) << 3 = 0
-	code_2 / code_3 = 2
-	code_3 – code_4 + 1 = 0
Since there are four variables that are checked by only three equations, we can choose any value for code_1, then calculate values for code_2 through code_4 based on the value we chose. A script that does this is shown below:

```
def codegen(nonce, a):
    b = -(nonce + a)
    c = int(b / 2)
    d = c + 1
    print("b: ", hex(b))
    print("c: ", hex(c))
    print("d: ", hex(d))
    print("Full code: ", hex(a), hex(b), hex(c), hex(d))

print("Enter nonce:")
n = int(input())
a = 0
if(n % 2 == 1): a = 1
codegen(n, a)
```

We can now connect to the challenge server, obtain the nonce, and run our solve script with the nonce as input. This gives us a launch code that we can enter when prompted.
 
 ![](/ctf_screenshots/launchcode_4.png)
 
The solve script returns a correct code, giving us the flag `shctf{Every-cUb1c-1nch-0f-spAce-is-a-m1racl3}`.
