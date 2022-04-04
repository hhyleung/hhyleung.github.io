---
title: "picoCTF 2022 - Reverse Engineering"
excerpt: "Writeup for the picoCTF 2022 - Reverse Engineering category"
last_modified_at: 2022-04-04
stickies: true
stickies_path: "/assets/stickies/picoctf.png"
toc: true
toc_label: "Challenges"
toc_sticky: true
categories:
  - Writeups
tags:
  - CTF
---

## Reverse Engineering
### file-run1
`100 points` `5525 solves`

> A program has been provided to you, what happens if you try to run it on the command line?<br>
> Download the program [here](https://artifacts.picoctf.net/c/310/run).

Granted permission to run the program and the flag was returned.

```bash
└─$ chmod +x ./run

└─$ ./run
The flag is: picoCTF{U51N6_Y0Ur_F1r57_F113_47cf2b7b}
```

Flag: `picoCTF{U51N6_Y0Ur_F1r57_F113_47cf2b7b}`

<br>

### file-run2
`100 points` `5292 solves`

> Another program, but this time, it seems to want some input. What happens if you try to run it on the command line with input "Hello!"?<br>
> Download the program [here](https://artifacts.picoctf.net/c/353/run).

Granted permission to run the program and ran it with the input `"Hello!"` to obtain the flag.

```bash
└─$ chmod +x run

└─$ ./run
Run this file with only one argument.

└─$ ./run "Hello!"
The flag is: picoCTF{F1r57_4rgum3n7_f65ed63e}
```

Flag: `picoCTF{F1r57_4rgum3n7_f65ed63e}`

<br>

### GDB Test Drive
`100 points` `4321 solves`

> `binary` `gdb`<br>
> Can you get the flag?<br>
> Download this [binary](https://artifacts.picoctf.net/c/117/gdbme).<br>
> Here's the test drive instructions:<br>
> ```bash
> $ chmod +x gdbme
> $ gdb gdbme
> (gdb) layout asm
> (gdb) break *(main+99)
> (gdb) run
> (gdb) jump *(main+104)
> ```

Followed the commands provided and obtained the flag.

Flag: `picoCTF{d3bugg3r_dr1v3_7776d758}`

<br>

### patchme.py
`100 points` `4482 solves`

> Can you get the flag?<br>
> Run this [Python program](https://artifacts.picoctf.net/c/388/patchme.flag.py) in the same directory as this [encrypted flag](https://artifacts.picoctf.net/c/388/flag.txt.enc).

The python file reveals the password as `ak98-=90adfjhgj321sleuth9000`.

```python
def level_1_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    # remove if to bypass password checking
    if( user_pw == "ak98" + \
                   "-=90" + \
                   "adfjhgj321" + \
                   "sleuth9000"):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), "utilitarian")
        print(decryption)
        return
    print("That password is incorrect")
```

Either provide the password to the program or remove the password checking part in the program to get the flag.

```bash
└─$ python patchme.flag.py 
Please enter correct password for flag: ak98-=90adfjhgj321sleuth9000
Welcome back... your flag, user:
picoCTF{p47ch1ng_l1f3_h4ck_21d62e33}
```

Flag: `picoCTF{p47ch1ng_l1f3_h4ck_21d62e33}`

<br>

### Safe Opener
`100 points` `4364 solves`

> Can you open this safe?<br>
> I forgot the key to my safe but this [program](https://artifacts.picoctf.net/c/463/SafeOpener.java) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?<br>
> Put the password you recover into the picoCTF flag format like:<br>
> `picoCTF{password}`

The java file reveals the Base64 encoded password, which can be decoded using [CyberChef](https://gchq.github.io/CyberChef/#recipe=From_Base64('A-Za-z0-9%2B/%3D',true)&input=Y0d3ellYTXpYMnd6ZEY5dE0xOHhiblF3WDNSb00xOXpZV1l6).

```java
Base64.Encoder encoder = Base64.getEncoder();
...
public static boolean openSafe(String password) {
    String encodedkey = "cGwzYXMzX2wzdF9tM18xbnQwX3RoM19zYWYz";

    if (password.equals(encodedkey)) {
        System.out.println("Sesame open");
        return true;
    }
    else {
        System.out.println("Password is incorrect\n");
        return false;
    }
}
```

Flag: `picoCTF{pl3as3_l3t_m3_1nt0_th3_saf3}`

<br>

### unpackme.py
`100 points` `3455 solves`

> `packing`<br>
> Can you get the flag?<br>
> Reverse engineer this [Python program](https://artifacts.picoctf.net/c/466/unpackme.flag.py).

The program was encrypted and it is decrypted to plaintext before execution. Add `print(plain)` to reveal the program in plaintext.

```python
import base64
from cryptography.fernet import Fernet

payload = b'gAAAAABiMD09KmaS5E6AQNpRx1_qoXOBFpSny3kyhr8Dk_IEUu61Iu0TaSIf8RCyf1LJhKUFVKmOt2hfZzynRbZ_fSYYN_OLHTTIRZOJ6tedEaK6UlMSkYJhRjAU4PfeETD-8gDOA6DQ8eZrr47HJC-kbyi3Q5o3Ba28mutKCAkwrqt3gYOY9wp3dWYSWzP4Tc3NOYWfu-SJbW997AM8GA-APpGfFrf9f7h0VYcdKOKu4Vq9zjJwmTG2VXWFET-pkF5IxV3ZKhz36L5IvZy1dVZXqaMR96lovw=='

key_str = 'correctstaplecorrectstaplecorrec'
key_base64 = base64.b64encode(key_str.encode())
f = Fernet(key_base64)
plain = f.decrypt(payload)
# print payload in plaintext
print(plain)
exec(plain.decode())
```

The decrypted program revealed the password as `batteryhorse` followed by the flag displayed in plaintext.

```bash
└─$ python unpackme.flag.py 
b"\npw = input('What\\'s the password? ')\n\nif pw == 'batteryhorse':\n  print('picoCTF{175_chr157m45_85f5d0ac}')\nelse:\n  print('That password is incorrect.')\n\n"
What's the password? batteryhorse
picoCTF{175_chr157m45_85f5d0ac}
```

Flag: `picoCTF{175_chr157m45_85f5d0ac}`

<br>

### bloat.py
`200 points` `3315 solves`

> `obfuscation`<br>
> Can you get the flag?<br>
> Run this [Python program](https://artifacts.picoctf.net/c/430/bloat.flag.py) in the same directory as this [encrypted flag](https://artifacts.picoctf.net/c/430/flag.txt.enc).

The python code is hard to read as the names for function and variable are not self-explanatory, and the strings are composed by getting one character at a time from the defined array.

Nevertheless, there was only one `if` checking mechanism that is very likely to be the password. Simply add 

```python
a = "!\"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ"+ \
            "[\\]^_`abcdefghijklmnopqrstuvwxyz{|}~ "
def arg133(arg432):
  # the only if checking mechanism
  if arg432 == a[71]+a[64]+a[79]+a[79]+a[88]+a[66]+a[71]+a[64]+a[77]+a[66]+a[68]:
    return True
  else:
    print(a[51]+a[71]+a[64]+a[83]+a[94]+a[79]+a[64]+a[82]+a[82]+a[86]+a[78]+\
a[81]+a[67]+a[94]+a[72]+a[82]+a[94]+a[72]+a[77]+a[66]+a[78]+a[81]+\
a[81]+a[68]+a[66]+a[83])
    sys.exit(0)
    return False
...
# print password before executinh other functions
print(a[71]+a[64]+a[79]+a[79]+a[88]+a[66]+a[71]+a[64]+a[77]+a[66]+a[68])
arg444 = arg132()
arg432 = arg232()
arg133(arg432)
arg112()
arg423 = arg111(arg444)
print(arg423)
sys.exit(0)
```

The password is revealed to be `happychance` and printed before the password prompt, provide the password and the flag is returned.

```bash
└─$ python bloat.flag.py 
happychance
Please enter correct password for flag: happychance
Welcome back... your flag, user:
picoCTF{d30bfu5c4710n_f7w_5e14b257}
```

Flag: `picoCTF{d30bfu5c4710n_f7w_5e14b257}`

<br>

### Fresh Java
`200 points` `3271 solves`

> `Java`<br>
> Can you get the flag?<br>
> Reverse engineer this [Java program](https://artifacts.picoctf.net/c/209/KeygenMe.class).

Decompiled the file using [http://www.javadecompilers.com/](http://www.javadecompilers.com/) and the decompiled java code revealed that there is a checking mechanism for each character of the flag.

```java
import java.util.Scanner;

public class KeygenMe {
    public static void main(final String[] array) {
        final Scanner scanner = new Scanner(System.in);
        System.out.println("Enter key:");
        final String nextLine = scanner.nextLine();
        if (nextLine.length() != 34) {
            System.out.println("Invalid key");
            return;
        }
        if (nextLine.charAt(33) != '}') {
            System.out.println("Invalid key");
            return;
        }
        ...
        if (nextLine.charAt(0) != 'p') {
            System.out.println("Invalid key");
            return;
        }
        System.out.println("Valid key");
    }
}
```

Saved the decompiled java code into a text file and used `grep` to get the flag characters, reverse the order, and concatenated it into one string. The flag was returned and verified with the program.

```bash
└─$ grep \' KeygenMe.txt | cut -d "'" -f2 | tac | awk '{print}' ORS=''
picoCTF{700l1ng_r3qu1r3d_2bfe1a0d}

└─$ java KeygenMe
Enter key:
picoCTF{700l1ng_r3qu1r3d_2bfe1a0d} 
Valid key
```

Flag: `picoCTF{700l1ng_r3qu1r3d_2bfe1a0d}`

<br>
