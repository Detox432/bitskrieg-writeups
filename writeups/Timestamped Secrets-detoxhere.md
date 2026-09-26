# Timestamped Secrets - Cryptography


## Approach
Contents of encyrption.py ![cat](image-17.png) show us that the time at which it was encrypted is the seed is hashed to generate the key using SHA256(str(timestamp))encode() which is then trunctated to 16 byets for AES-128. message.txt also gives us the given timestamp and the ciphertext that we need to decode

## Solution
Since we understand how timestamp was being used to generate the key, the ciphertext from message.txt can easily be decoded. I wrote a short python script where it generates the key from the same way except this time using the timestamp at which the ciphertext was encrypted
![decryption.py](image-18.png). Running this python script gives us the flag ![flag](image-19.png)

## Flag
picoCTF{sa3S_sEc9t_194672d0}


## Takeaway
Tracing the code is very important to understand how a variable is being manipulated exactly. 
