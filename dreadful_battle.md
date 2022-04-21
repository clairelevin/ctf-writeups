# Dreadful Battle (Space Heroes CTF 2022)
 
This challenge presents us with a “battle” that we must win by entering the correct text at each prompt. Looking at the challenge file in Binary Ninja, we can see how the correct response is evaluated:
 
![](/ctf_screenshots/dreadful_1.png)

At each stage, the “Battle” function calls a function called “TurnAction,” which takes in two parameters: the user input, and the number of turns that have passed so far.
 
![](/ctf_screenshots/dreadful_2.png)
![](/ctf_screenshots/dreadful_3.png)
 
With each turn, some combination of the functions “ObstacleOne,” “ObstacleTwo,” and “ObstacleThree” are called on the user input, and the result is compared to a specific string. The three “Obstacle” functions were found to do the following:
-	ObstacleOne takes the index of each character in the string and adds it to the value of that character.
-	ObstacleTwo takes the index of each character in the string and XORs it with that character.
-	ObstacleThree takes the index of each character and subtracts it from that character, then adds 7.
Since all three “Obstacle” functions are reversible and we know what the result of each turn is supposed to be, we can write a solve script that performs the inverse of the operations performed in each turn. This script is given below:

```
def oneInverse(theString):
    copy = bytearray(theString, 'ascii')
    for i in range(len(copy)):
        copy[i] -= i
    return copy.decode(errors='backslashreplace')

def twoInverse(theString):
    copy = bytearray(theString, 'ascii')
    for i in range(len(copy)):
        copy[i] = copy[i] ^ i
    return copy.decode(errors='backslashreplace')

def threeInverse(theString):
    copy = bytearray(theString, 'ascii')
    for i in range(len(copy)):
        copy[i] = copy[i] + i + 7
    return copy.decode(errors='backslashreplace')

turn_results = ['<aZk`^', ';eZnu', '6_RWW', 'DaQYWd', '4_Qfb', '<aZk`^', 'Fkvk1']
turn_operations = [[3,1,2,2], [1,2,1,3], [3,2,1,3], [3,1,3,2], [3,1,1,3,2], [3,1,2,2], [1,1,2,1]]

resultStr = ""
for i in range(len(turn_results)):
    s = turn_results[i]
    operations_to_do = turn_operations[i]
    operations_to_do.reverse()
    for op in operations_to_do:
        if(op == 1):
            s = oneInverse(s)
        elif(op == 2):
            s = twoInverse(s)
        else:
            s = threeInverse(s)
    resultStr = resultStr + s + ' '

print(resultStr)
```

This gets us the following:

`Charge BlasXq.' Dodge Rocket Blast Charge Fire!`

Assuming “BlasXq.'” is a typo and the correct result is “Blast”, we can now enter the right value at each prompt. With every round, more of the flag is printed out.

![](/ctf_screenshots/dreadful_4.png)
 
Concatenating the values printed at the end of each round, we obtain the flag: `shctf{Charge_Beeeeeeeeeeaaaaaam!}`
