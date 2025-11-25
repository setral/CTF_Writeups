# The First Challenge is in the description of the Kickstarter
<img width="607" height="463" alt="image" src="https://github.com/user-attachments/assets/bffcab9a-3449-43e1-bb25-69615bc462bf" />

## Challenge #1 of 4:

01101000 01110100 01110100 01110000 01110011 00111010 00101111 00101111 01101101 01100011 01110100 01100110 00101110 01101001 01101111 00101111 00110110 01100110 00110101 01100010 00111001 00111001 01100110

Looking at the 1s and 0s, being in groups of eight, indicate this is likely Binary.

Converting from Binary to text, we get: 104 116 116 112 115 58 47 47 109 99 116 102 46 105 111 47 54 102 53 98 57 57 102

Since the binary text converted to 3 digit numbers, this is likely ASCII.

Converting from ASCII to text, we get: https://mctf.io/6f5b99f

Access the URL to retrieve the bonus key AND the second part of the challenge.


## Second Part of Challenge 1
<img width="869" height="109" alt="image" src="https://github.com/user-attachments/assets/dc46e609-7bc9-4adf-a44b-eceaf70f39e5" />

Challenge URL: https://challenges2.tficomic.io/kickstarter-1/


The challenge page hints at what we need to do:
<img width="865" height="103" alt="image" src="https://github.com/user-attachments/assets/1e988df3-3c4c-4e32-b43f-546004c60538" />

The hint suggests we need to appear as Chrome version 476 (a future/nonexistent version).

This is a user-agent (UA) check.

Easiest path: Spoof the user-agent in Chrome DevTools
1. Open the URL in the Chrome Browser
2. Press **F12** to access DevTools
3. Click on **Network Conditions**, in the lower middle of the window
4. Scroll down to **User Agent** and uncheck **Use default browser**
5. Edit the user agent line to show Chrome 476

Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/476.0.0.0 Safari/537.36


<img width="804" height="267" alt="image" src="https://github.com/user-attachments/assets/dc592eb4-1541-41fc-90ef-2c637eae3759" />


Leave the Developer Console open and reload the page

If done successfully, the screen should change to:

<img width="743" height="104" alt="image" src="https://github.com/user-attachments/assets/2f1c16c9-82bf-4145-813b-83fd3413bd24" />


Congrats!
