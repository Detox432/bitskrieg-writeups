# Binary Digits - Forensics


## Approach
We recieved a digits.bin file, upon using file ![file digits.bin](image-9.png) tells us that this is not an actual binary file, just a ascii list of 0 and 1s, even using xxd digits.bin | less ![xxd](image-10.png) shows us that its a big string of 0 and 1 and theres nothing useful in this. I also tried using grep for the entire file to see if the flag is hidden somewhere in the middle ![grep](image-11.png) but it was of no use as well. To convert this ascii list of 0 and 1s to actual binary, I put the entire string in cyberchef and used From Binary to get the raw bytes of the file ![cyberchef](image-12.png).

## Solution
From this retrieved binary file, I converted into Hex using To Hex in cyberchef, essentially using xxd on the actual binary file. ![TO hex](image-13.png). This gave us the big clue that the starting 4 bits were FF D8 which are identifires for a JPEG file. Going back to the raw byte data and saving output to a file and naming it image.jpeg can be opened which gives us the hidden flag ![FLAG](<image (1).jpeg>).

## Flag
picoCTF{h1dd3n_1n_th3_b1n4ry_2c2db635}

## Takeaway
Using Cyberchef for fast conversions and always checking identifiers before saving output to know what type of file it is.
