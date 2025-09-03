# OGN - Challenge 1

## Link to the Challenge
<img width="924" height="465" alt="image" src="https://github.com/user-attachments/assets/0f093d8a-eda3-4584-a066-e1306871371b" />

There’s no puzzle here yet, just a challenge URL hidden at the bottom of the page.

tficomic.io/gun

### Don't forget to enter the bonus points!
On the challenge page is a bonus key **KEY{xxxxxx}**

Sign-up or Sign-in to https://metactf.com/join/future and click the BONUS button to submit it for extra points!

## On to the challenge!  
<img width="869" height="190" alt="image" src="https://github.com/user-attachments/assets/0b9da28c-2f6d-4b76-bf11-5d578ececc20" />

We are recreating Wheeler's attack on the smart gun system, just like in the comic!  

### What we need:  
1. A computer with **NC** (Netcat) on it (Netcat can be used maliciously, most AntiVirus will alert/remove it).  
   I suggest running a virtual machine, I used Oracle VirtualBox with a Kali Linux virtual machine.

   We will be using Netcat to connect to the console mentioned on the challenge page: **nc challenges.tficomic.io 7005**

   
3. The **console.py** file from the challenge page
4. Python3 installed **OR** a web based Python interpreter like: https://www.w3schools.com/python/trypython.asp?filename=demo_compiler

## Initial connection to the challenge console

<img width="557" height="475" alt="image" src="https://github.com/user-attachments/assets/b45b5092-e37a-4aff-a182-faf42295db95" />

We can't do much right now, we don't have the password.

Maybe there is a clue in the provided console.py?


## Reviewing the console.py
```
#!/usr/bin/python
import time

def main(): 
    flag = ''
    with open('./flag.txt', 'r') as f:
        flag = f.readline().strip()

    print("=========== Welcome to the USHKUYNIK smart rifle system! ===========", end="", flush=True)
    time.sleep(1)

    admin = False
    admin_pw_encrypted = '6d6e71775b7174727b7d6f6f536460506479774c677877656c4668727a717b40494f46565751545e'

    while True:
        print("\nWhat would you like to do?\n", flush=True)
        print("1. Activate FRIEND-OR-FOE system")
        print("2. Enter administrator password")
        print("3. Exit")
        user_in = input('> ')

        if user_in == '1':
            if admin:
                print('\nFRIEND-OR-FOE system activated.', flush=True)
                time.sleep(0.5)
                print(f'\nCongratulations! Here is the flag: {flag}')
                exit()
            else:
                print('\nERROR: Administrator privileges required.', flush=True)
                time.sleep(1)
        elif user_in == '2':
            print('\nPlease enter the administrator password: ', end="", flush=True)
            pw = input("")
            admin_pw = ''.join(chr(ord(c) ^ i) for i, c in enumerate(bytes.fromhex(admin_pw_encrypted).decode("utf-8")))
            if pw == admin_pw:
                admin = True 
                print('\nAdministrator password verified. Privileges updated.', flush=True)
                time.sleep(1)
            else:
                print('\nERROR: Incorrect administrator password', flush=True)
                time.sleep(1)
        elif user_in == '3':
            exit()
        else:
            print('\nInvalid option. Please try again', flush=True)
            time.sleep(1)


if __name__ == "__main__":
    main()
```

### What we know:
+ Console.py looks for a ./flag.txt
+ Console.py has an encrypted password
+ Console.py has basic options
  1. Activate FRIEND-OR-FOE system (Errors unless admin)
  2. Enter Admin Password (Entering password grants admin)
  3. Exit (End session)
+ Console.py displays the content of ./flag.txt when using option 1 after entering the admin password
+ Console.py checks the password against the encrypted password when you select option #2

## Extracting the Encrypted Password
Thankfully the console.py has almost everything we need.
+ **Encrypted Password:** admin_pw_encrypted = '6d6e71775b7174727b7d6f6f536460506479774c677877656c4668727a717b40494f46565751545e'
+ **Password Check:** admin_pw = ''.join(chr(ord(c) ^ i) for i, c in enumerate(bytes.fromhex(admin_pw_encrypted).decode("utf-8")))

To recover the password, we simply combine the decryption logic with the encrypted value and display the result.

By adding a `print` function we can achieve that!
```
admin_pw_encrypted = '6d6e71775b7174727b7d6f6f536460506479774c677877656c4668727a717b40494f46565751545e'
admin_pw = ''.join(chr(ord(c) ^ i) for i, c in enumerate(bytes.fromhex(admin_pw_encrypted).decode("utf-8")))
print(f"{admin_pw}")
```

If we run the above example either as a Python script file `.py` or through the web interpreter, we get the answer.

<img width="932" height="208" alt="image" src="https://github.com/user-attachments/assets/f0271e32-c860-4726-b013-ec2668261384" />

**most_trusted_in_the_smart_rifle_industry**

## Verifying access with the Password
1. Connect to the Challenge Console via NC: **nc challenges.tficomic.io 7005**
2. Enter the Admin Password: **most_trusted_in_the_smart_rifle_industry**
3. Activate the FRIEND-OR-FOE system

<img width="664" height="387" alt="image" src="https://github.com/user-attachments/assets/4f566299-da09-42a6-baca-287f18deb7d0" />

To claim the flag, go to the MetaCTF portal here: https://compete.metactf.com/300/problems

And enter the flag under "OGN - Challenge 1"
<img width="1112" height="190" alt="image" src="https://github.com/user-attachments/assets/02aca64d-6fe9-4136-8ecc-91df0e45459f" />


