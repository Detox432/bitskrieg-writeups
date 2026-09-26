# Secure Password Database - Reverse Engineering


## Approach
first used file on system.out, tells us that it is an exectuable, running system.out as ./system.out tells us to input a passowrd, inputting anything random then asks us to input the number of bytes of our password, inputting any number gives us our stored password in a form like this, When we input a large number of bytes as the length of our password, the code leaks and gives us the byte information of something else that is in the buffer ![system.out](image-20.png). I then also decompiled the code using ghida to find the main function where the password input and the buffer input functions look something like this ![main](image-22.png).![hash check](image-21.png) This is the important part where the function does the hash check. The big takeaways were that like my original test, inputting an a big length of byets leaks and displays extra information even though it is not the size of the password i inputted, also the hash has some extra hidden bytes that is stored in the memory. The hash function is also seen in ghidra  ![hash](image-23.png). and the make secret function tell us exactly how the secret is created ![makesecret](image-24.png)

## Solution
In the main function we see at the start a secret that lives at a given buffer which is pre defined in the code ![buffer](image-25.png) this is clearly what was retrieved when i inputted extra bytes that leaked this in the buffer. On running a controlled test by running system.out and inputting a password like hello and inputting buffer legnth to be 100 we see ![secret](image-26.png) the bytes 105 85 98 104 56 49 33 106 42 104 110 33 -86  where  the last -86 byte is something garbage, exclding that, when converted to ASCII gives us ![secret](image-27.png)
using a c script to get the actual hash, we can essentially just copy the entire hash function and use our parameters i.e. the string we recovered as secret to get what the actual hash is. ![script](image-28.png) this is the c code and running it gives us the hash ![hash](image-29.png). And with the following inputs we get this ![answer](image-30.png)

## Flag
academy{d0nt_trust_us3rs}

## Takeaway
Analysing each function after decompiling is very important in ghidra, The way hash functions are made can be used to reverse engineer the hashed output easily and We should always look out for oversights like allowing user to view more byets than the password they have entered allowing them to look into the buffer.
