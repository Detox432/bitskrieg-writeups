# Challenge Name - category


## Approach
First I started by inspecting the source code of the website to see if I could find anything hidden or useful, all of it was pretty basic in terms of the html and css, Since no credentials were given, i registered a custom user with username:hello and password:123 

<img width="737" height="504" alt="Screenshot_20260927_153603" src="https://github.com/user-attachments/assets/0dc95c62-8722-4f30-b4e2-93e10d6d7015" />
Also checking the source code of the register page didnt give me anything useful. Then using these credentials i logged into this account to see the home page. A big hint was already given that something was hidden at /sessions <img width="702" height="77" alt="Screenshot_20260927_153852" src="https://github.com/user-attachments/assets/3859510c-2fe6-49cd-9410-8ece764ad955" />.



## Solution
Going to /sessions reveals what was said in the description, that the session of the admin was never logged out and the cookie was saved there which we could view <img width="903" height="84" alt="Screenshot_20260927_154133" src="https://github.com/user-attachments/assets/64037f44-3d7e-47e1-8cb0-581f2d15007e" /> from this we get the cookie of the admin user and since its never logged out ('_permanent':True) we can just change our current cookie to the admin cookie to log into the admin session.
<img width="922" height="661" alt="Screenshot_20260927_154320" src="https://github.com/user-attachments/assets/80afc8b6-ee3a-437e-983b-5b64c73344c2" />
Refreshing the page we get the admin dashboard and the flag


## Flag
academy{s3t_s3ss10n_3xp1rat10n5_e3a46efc}

## Takeaway
Always check for access points like /sessions or /robots.txt and others to look out for extra information.
