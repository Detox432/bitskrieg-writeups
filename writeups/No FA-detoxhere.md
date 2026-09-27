# No FA - Web Exploitation


## Approach
First i started by examining the source code of the login page, found nothing useful and also since we didnt have any credentials given to us I moved on to check the leaked data that was given in users.db. I used sqlitebrowser to open this database 
<img width="1436" height="798" alt="Screenshot_20260927_184156" src="https://github.com/user-attachments/assets/b9b8eab0-a764-4c24-ac6b-f3f98e4411b6" />
It was a list of 20 users along with their encrypted password, I found the encrypted password for the admin user. Since I did not know how this password was encrypted, I moved on to read the flask backend source code. It was clear that logging into the admin user would give us the flag so the goal was to find a way to log into admin
<img width="446" height="98" alt="Screenshot_20260927_184329" src="https://github.com/user-attachments/assets/52521d79-dd9f-46ed-856f-c850b2c5d901" />.
I also saw that for accounts with 2FA enabled (admin was the only one in this case), a random OTP would be generated between 1000 and 9999 for you to login. This otp was also being saved in the sessions dictionary that flask uses.
<img width="791" height="288" alt="Screenshot_20260927_184852" src="https://github.com/user-attachments/assets/43c2c2c8-85e9-41ed-b512-df990d663f05" />


## Solution
Looking at the code it was clear how the passwords were being encrypted, it was using sha256 
<img width="775" height="22" alt="Screenshot_20260927_184956" src="https://github.com/user-attachments/assets/14511cd0-6893-4e60-82a3-565b6e473acb" /> To decode this, i put the password into crackstation.net and it gave me the output "apple@123" 
<img width="1168" height="109" alt="Screenshot_20260927_185048" src="https://github.com/user-attachments/assets/cdeb92f3-af8f-4d14-933b-f1ec13019acc" />
After logging into the account, we needed the otp. I fond brute forcing via burp suite intruder to be very slow so instead since otp was being saved into sessions dictionary of flask, the cookie of my session already contained the otp inside it, it was just encrypted. From googling a bit i learned that the flask cookie i had .eJwty0EKgCAQAMC_7FlC0RL9TEguIrQqup6iv-eh68A8cNeUMIIH7hNBQOV2Drw68jItD_0bZ8LBgRp4ZZ3clTFWbtoo7ZwVMAf2EghXCpFygfcDKNMcDg.arkVWQ.zCeLq1ejHwcgqbSbQp1yQHwPm_o Was structured where eJwty0EKgCAQAMC_7FlC0RL9TEguIrQqup6iv-eh68A8cNeUMIIH7hNBQOV2Drw68jItD_0bZ8LBgRp4ZZ3clTFWbtoo7ZwVMAf2EghXCpFygfcDKNMcDg was encrypted payload of my session and the rest were the timestamp and the hmac signature at the end. Since I only need to read what the otp is, putting this payload into cyberchef and using From Base64 and Zlib Inflat i got the otp, Here i had to use url safe version of base64 decode to mantain all the data int he cookie.
<img width="1539" height="847" alt="Screenshot_20260927_190114" src="https://github.com/user-attachments/assets/8d34ccb3-999e-41c0-8dab-43ab78d0ba48" />
Using this otp fast since there was a 120s timeout, i got the flag


<img width="1919" height="976" alt="Screenshot_20260927_183928" src="https://github.com/user-attachments/assets/83af6ce1-1755-408a-a040-06a987f977f0" />

## Flag
academy{n0_r4t3_n0_4uth_b8c7ed63}

## Takeaway

