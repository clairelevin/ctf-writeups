# Shopkeeper 2 (HackPack CTF 2022)
This challenge presents us with a menu of options: “Buy”, “Sell”, “View Your Inventory”, and “Leave Shop.” Our goal is to obtain 100 coins in order to buy the key to the flag.
 
 ![](/ctf_screenshots/shopkeeper_1.png)
 ![](/ctf_screenshots/shopkeeper_2.png)
 
After some experimentation with different invalid inputs, we find that the program handles the input of a blank line incorrectly. If we try to buy apples and enter a blank line, we end up with     -38 apples and 86 coins. This can be repeated indefinitely to get us as many coins as we want.

 ![](/ctf_screenshots/shopkeeper_3.png)

After we buy the key to the flag, the flag is printed when we check our inventory: `flag{g00d_job_y0u_b3at_7he_sh0pk3eper}`

 ![](/ctf_screenshots/shopkeeper_4.png)
