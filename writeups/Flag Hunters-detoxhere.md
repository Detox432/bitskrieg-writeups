# Flag Hunters - Reverse Engineering


## Approach
First reading the source code its clear that the flag is right there at the start of the entire string that is being printed but the function is called from [VERSE1] only which is the reason we never see the flag verse show up ![function called](image-32.png). In the lyric reader logic keywords like REFRAIN, RETURN and CROWD that each serve different functions. REFRAIN acts like a function call, jumping to the chorus part of the song, RETURN is a placeholder that gets filled in with a line number so it knows where to jump back to once the chorus is done and CROWD allowed the user to input something amidst the song that got echoed later throughout the song ![crowd](image-33.png).

## Solution
Looking at the code carefully we see that whatever is inputted in CROWD gets added to the entire string of the song which is how it gets printed out in the later choruses. Since all the checks for the keywords run on the entire string again, essentially we can input these keywords that change what the code does itself. The important keyword here is RETURN where it allows us to change the current line to something that we can decide, in this case since the flag chorus sits rigth at the start, if we can get the function to read RETURN 0 then we would be able to get the code. Another important observation is that it splits the line when printing it by ";" ![line split](image-34.png). Since normal RETURN 0 wont work as it doesnt get read as a separate line, we need to input ;RETURN 0 in the crowd field so that it get read as a different line and the following RETURN 0 causes the function to return us to line 0 where the flag verse is.![flag](image-31.png)

## Flag
academy{70637h3r_f0r3v3r_42783b07}

## Takeaway
Very important to test for inputs that can change the logic of the code using keywords etc.
