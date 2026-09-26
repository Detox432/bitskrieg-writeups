# StegoRSA - Cryptography


## Approach
First i tried doing file on the image.jpg file ![file](image-14.png) This gave us this weird comment, upon using exiftool it becomes more clear that this is a long hex string that is hidden in the comments ![exiftool](image-15.png)

## Solution
cyberchefs magic wand tool suggested that using From Hex will give us something useful ![from hex](image-16.png), upon using this we obtain the private key that will be used to decode flag.enc. Saving the output to a file called key.pem (standard extension for private keys). I used "openssl pkeyutl -decrypt -inkey key.pem -in flag.enc" to decrypt the encrypted file.

## Flag
picoCTF{rs4_k3y_1n_1mg_66388eb3}

## Takeaway
Cyberchef magic tool is very useful, always check metadata for hidden information.
