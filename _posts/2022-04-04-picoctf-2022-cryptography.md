---
title: "picoCTF 2022 - Cryptography"
excerpt: "Writeup for the picoCTF 2022 - Cryptography category"
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

## Cryptography
### basic-mod1
`100 points` `5882 solves`

> We found this weird message being passed around on the servers, we think we have a working decryption scheme.
> 
> ```text
> 91 322 57 124 40 406 272 147 239 285 353 272 77 110 296 262 299 323 255 337 150 102
> ```
> 
> Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.<br>
> Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)

```python
set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_"
msg = "91 322 57 124 40 406 272 147 239 285 353 272 77 110 296 262 299 323 255 337 150 102"
msg = msg.split(" ")
flag = "picoCTF{"

for num in msg:
    mod = int(num) % 37
    flag += set[mod]

print(flag + "}")
```

Flag: `picoCTF{R0UND_N_R0UND_ADD17EC2}`

<br>

### basic-mod2
`100 points` `4377 solves`

> A new modular challenge!
> 
> ```text
> 104 290 356 313 262 337 354 229 146 297 118 373 221 359 338 321 288 79 214 277 131 190 377
> ```
> 
> Take each number mod 41 and find the modular inverse for the result. Then map to the following character set: 1-26 are the alphabet, 27-36 are the decimal digits, and 37 is an underscore.<br>
> Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)

```python
set = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789_"
msg = "104 290 356 313 262 337 354 229 146 297 118 373 221 359 338 321 288 79 214 277 131 190 377"
msg = msg.split(" ")
flag = "picoCTF{"

for num in msg:
    mod = int(num) % 41
    inv = pow(mod, -1, 41)
    flag += set[inv - 1]

print(flag + "}")
```

Flag: `picoCTF{1NV3R53LY_H4RD_8A05D939}`

<br>

### credstuff
`100 points` `4512 solves`

> We found a leak of a blackmarket website's login credentials. Can you find the password of the user `cultiris` and successfully decrypt it?<br>
> Download the leak [here](https://artifacts.picoctf.net/c/534/leak.tar).

The first user in `usernames.txt` corresponds to the first password in `passwords.txt`. The second user corresponds to the second password, and so on.

Searched for the user `cultiris` locating at line `378` and obtained its corresponding password as `cvpbPGS{P7e1S_54I35_71Z3}`.

```bash
└─$ grep -n cultiris leak/usernames.txt 
378:cultiris

└─$ sed -n 378p leak/passwords.txt      
cvpbPGS{P7e1S_54I35_71Z3}
```

The password looks like an encoded flag, which was decoded as ROT13 cipher using [CyberChef](https://gchq.github.io/CyberChef/#recipe=ROT13(true,true,false,13)&input=Y3ZwYlBHU3tQN2UxU181NEkzNV83MVozfQ).

Flag: `picoCTF{C7r1F_54V35_71M3}`

<br>

### morse-code
`100 points` `4323 solves`

> `morse_code`<br>
> Morse code is well known. Can you decrypt this?<br>
> Download the file [here](https://artifacts.picoctf.net/c/235/morse_chal.wav).<br>
> Wrap your answer with picoCTF{}, put underscores in place of pauses, and use all lowercase.

Uploaded the wav file to [https://morsecode.world/international/decoder/audio-decoder-adaptive.html](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) to decode the morse code into `WH47 H47H 90D W20U9H7`. Added underscore in between and transformed into lowercase to obtain the flag.

Flag: `picoCTF{wh47_h47h_90d_w20u9h7}`

<br>

### rail-fence
`100 points` `4177 solves`

> A type of transposition cipher is the rail fence cipher, which is described [here](https://en.wikipedia.org/wiki/Rail_fence_cipher). Here is one such cipher encrypted using the rail fence with 4 rails. Can you decrypt it?
> 
> ```text
> Ta _7N6DDDhlg:W3D_H3C31N__0D3ef sHR053F38N43D0F i33___NA
> ```
> 
> Put the decoded message in the picoCTF flag format, `picoCTF{decoded_message}`.

The flag was decrypted as rail fence cipher with 4 keys using [CyberChef](https://gchq.github.io/CyberChef/#recipe=Rail_Fence_Cipher_Decode(4,0)&input=VGEgXzdONkRERGhsZzpXM0RfSDNDMzFOX18wRDNlZiBzSFIwNTNGMzhONDNEMEYgaTMzX19fTkE).

Flag: `picoCTF{WH3R3_D035_7H3_F3NC3_8361N_4ND_3ND_D00AFDD3}`

<br>

### substitution0
`100 points` `4571 solves`

> `Substitution`<br>
> A message has come in but it seems to be all scrambled. Luckily it seems to have the key at the beginning. Can you crack this substitution cipher?
> 
> ```text
> VOUHMJLTESZCDKWIXNQYFAPGBR 
> 
> Tmnmfiwk Cmlnvkh vnwqm, peyt v lnvam vkh qyvymcb ven, vkh onwflty dm ytm ommycm
> jnwd v lcvqq uvqm ek pteut ey pvq mkucwqmh. Ey pvq v omvfyejfc quvnvovmfq, vkh, vy
> ytvy yedm, fkzkwpk yw kvyfnvceqyq—wj uwfnqm v lnmvy inerm ek v quemkyejeu iweky
> wj aemp. Ytmnm pmnm ypw nwfkh ocvuz qiwyq kmvn wkm mgynmdeyb wj ytm ovuz, vkh v
> cwkl wkm kmvn ytm wytmn. Ytm quvcmq pmnm mgummheklcb tvnh vkh lcwqqb, peyt vcc ytm
> viimvnvkum wj ofnkeqtmh lwch. Ytm pmelty wj ytm ekqmuy pvq amnb nmdvnzvocm, vkh,
> yvzekl vcc yteklq ekyw uwkqehmnvyewk, E uwfch tvnhcb ocvdm Sfieymn jwn teq wiekewk
> nmqimuyekl ey.
> 
> Ytm jcvl eq: ieuwUYJ{5FO5717F710K_3A0CF710K_357OJ9JJ}
> ```

The last string is very likely to be the flag in the format `picoCTF{...}`, which gave a few substitution key that can be used to decode the message using [CyberChef](https://gchq.github.io/CyberChef/#recipe=To_Lower_case()Substitute('ieuwuyj','picoctf')&input=Vk9VSE1KTFRFU1pDREtXSVhOUVlGQVBHQlIgCgpUbW5tZml3ayBDbWxudmtoIHZud3FtLCBwZXl0IHYgbG52YW0gdmtoIHF5dnltY2IgdmVuLCB2a2ggb253Zmx0eSBkbSB5dG0gb21teWNtCmpud2QgdiBsY3ZxcSB1dnFtIGVrIHB0ZXV0IGV5IHB2cSBta3Vjd3FtaC4gRXkgcHZxIHYgb212ZnllamZjIHF1dm52b3ZtZnEsIHZraCwgdnkKeXR2eSB5ZWRtLCBma3prd3BrIHl3IGt2eWZudmNlcXlx4oCUd2ogdXdmbnFtIHYgbG5tdnkgaW5lcm0gZWsgdiBxdWVta3llamV1IGl3ZWt5CndqIGFlbXAuIFl0bW5tIHBtbm0geXB3IG53ZmtoIG9jdnV6IHFpd3lxIGttdm4gd2ttIG1neW5tZGV5YiB3aiB5dG0gb3Z1eiwgdmtoIHYKY3drbCB3a20ga212biB5dG0gd3l0bW4uIFl0bSBxdXZjbXEgcG1ubSBtZ3VtbWhla2xjYiB0dm5oIHZraCBsY3dxcWIsIHBleXQgdmNjIHl0bQp2aWltdm52a3VtIHdqIG9mbmtlcXRtaCBsd2NoLiBZdG0gcG1lbHR5IHdqIHl0bSBla3FtdXkgcHZxIGFtbmIgbm1kdm56dm9jbSwgdmtoLAp5dnpla2wgdmNjIHl0ZWtscSBla3l3IHV3a3FlaG1udnlld2ssIEUgdXdmY2ggdHZuaGNiIG9jdmRtIFNmaWV5bW4ganduIHRlcSB3aWVrZXdrCm5tcWltdXlla2wgZXkuCgpZdG0gamN2bCBlcTogaWV1d1VZSns1Rk81NzE3RjcxMEtfM0EwQ0Y3MTBLXzM1N09KOUpKfQ).

For the words in the last line `Ytm jcvl eq`, with each of the first letter decoded to `Ttm fcvl iq,` it was reasonable to guess that the plaintext is `The flag is`, which gave a few more keys.

The first line was then partially decoded as `AOCHEFGHISZLDKOPXNSTFAPGBR`, which the first few decoded letter resulted to a bold guess that `VOUHMJLTESZCDKWIXNQYFAPGBR` is the substitution key for all alphabets. It was then used in [CyberChef](https://gchq.github.io/CyberChef/#recipe=Substitute('VOUHMJLTESZCDKWIXNQYFAPGBRvouhmjlteszcdkwixnqyfapgbr','ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz')&input=Vk9VSE1KTFRFU1pDREtXSVhOUVlGQVBHQlIgCgpUbW5tZml3ayBDbWxudmtoIHZud3FtLCBwZXl0IHYgbG52YW0gdmtoIHF5dnltY2IgdmVuLCB2a2ggb253Zmx0eSBkbSB5dG0gb21teWNtCmpud2QgdiBsY3ZxcSB1dnFtIGVrIHB0ZXV0IGV5IHB2cSBta3Vjd3FtaC4gRXkgcHZxIHYgb212ZnllamZjIHF1dm52b3ZtZnEsIHZraCwgdnkKeXR2eSB5ZWRtLCBma3prd3BrIHl3IGt2eWZudmNlcXlx4oCUd2ogdXdmbnFtIHYgbG5tdnkgaW5lcm0gZWsgdiBxdWVta3llamV1IGl3ZWt5CndqIGFlbXAuIFl0bW5tIHBtbm0geXB3IG53ZmtoIG9jdnV6IHFpd3lxIGttdm4gd2ttIG1neW5tZGV5YiB3aiB5dG0gb3Z1eiwgdmtoIHYKY3drbCB3a20ga212biB5dG0gd3l0bW4uIFl0bSBxdXZjbXEgcG1ubSBtZ3VtbWhla2xjYiB0dm5oIHZraCBsY3dxcWIsIHBleXQgdmNjIHl0bQp2aWltdm52a3VtIHdqIG9mbmtlcXRtaCBsd2NoLiBZdG0gcG1lbHR5IHdqIHl0bSBla3FtdXkgcHZxIGFtbmIgbm1kdm56dm9jbSwgdmtoLAp5dnpla2wgdmNjIHl0ZWtscSBla3l3IHV3a3FlaG1udnlld2ssIEUgdXdmY2ggdHZuaGNiIG9jdmRtIFNmaWV5bW4ganduIHRlcSB3aWVrZXdrCm5tcWltdXlla2wgZXkuCgpZdG0gamN2bCBlcTogaWV1d1VZSns1Rk81NzE3RjcxMEtfM0EwQ0Y3MTBLXzM1N09KOUpKfQ) to decode the whole message and indeed it was the key and the message was decoded successfully, with the flag as the last string.

```text
ABCDEFGHIJKLMNOPQRSTUVWXYZ 

Hereupon Legrand arose, with a grave and stately air, and brought me the beetle
from a glass case in which it was enclosed. It was a beautiful scarabaeus, and, at
that time, unknown to naturalists—of course a great prize in a scientific point
of view. There were two round black spots near one extremity of the back, and a
long one near the other. The scales were exceedingly hard and glossy, with all the
appearance of burnished gold. The weight of the insect was very remarkable, and,
taking all things into consideration, I could hardly blame Jupiter for his opinion
respecting it.

The flag is: picoCTF{5UB5717U710N_3V0LU710N_357BF9FF}
```

Flag: `picoCTF{5UB5717U710N_3V0LU710N_357BF9FF}`

<br>

### substitution1
`100 points`  `3535 solves`

> `Substitution_cipher`<br>
> A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.
> 
> ```text
> OYAt (txwsy aws ompyksb yxb ajmf) msb m yupb wa owzpkybs tboksgyu owzpbygygwd. Owdybtymdyt msb psbtbdybr lgyx m tby wa oxmjjbdfbt lxgox ybty yxbgs osbmygegyu, yboxdgomj (mdr fwwfjgdf) tqgjjt, mdr pswhjbz-twjegdf mhgjgyu. Oxmjjbdfbt ktkmjju owebs m dkzhbs wa omybfwsgbt, mdr lxbd twjebr, bmox ugbjrt m tysgdf (omjjbr m ajmf) lxgox gt tkhzgyybr yw md wdjgdb towsgdf tbsegob. OYAt msb m fsbmy lmu yw jbmsd m lgrb mssmu wa owzpkybs tboksgyu tqgjjt gd m tmab, jbfmj bdegswdzbdy, mdr msb xwtybr mdr pjmubr hu zmdu tboksgyu fswkpt mswkdr yxb lwsjr aws akd mdr psmoygob. Aws yxgt pswhjbz, yxb ajmf gt: pgowOYA{AS3CK3DOU_4774OQ5_4S3_O001_6B0659AH}
> ```

Similar to the above, the last part was first used to decode as `the flag is: picoCTF`. It was easy to read through the partially decoded message to make guesses for additional keys. The message was decoded successfully using [CyberChef](https://gchq.github.io/CyberChef/#recipe=Substitute('pgowyaxbjmftksuzdrleqhcPGOWYAXBJMFTKSUZDRLEQHC','picotfhelagsurymndwvkbqPICOTFHELAGSURYMNDWVKBQ')&input=T1lBdCAodHh3c3kgYXdzIG9tcHlrc2IgeXhiIGFqbWYpIG1zYiBtIHl1cGIgd2Egb3d6cGt5YnMgdGJva3NneXUgb3d6cGJ5Z3lnd2QuIE93ZHlidHltZHl0IG1zYiBwc2J0YmR5YnIgbGd5eCBtIHRieSB3YSBveG1qamJkZmJ0IGx4Z294IHlidHkgeXhiZ3Mgb3NibXlnZWd5dSwgeWJveGRnb21qIChtZHIgZnd3ZmpnZGYpIHRxZ2pqdCwgbWRyIHBzd2hqYnotdHdqZWdkZiBtaGdqZ3l1LiBPeG1qamJkZmJ0IGt0a21qanUgb3dlYnMgbSBka3poYnMgd2Egb215YmZ3c2didCwgbWRyIGx4YmQgdHdqZWJyLCBibW94IHVnYmpydCBtIHR5c2dkZiAob21qamJyIG0gYWptZikgbHhnb3ggZ3QgdGtoemd5eWJyIHl3IG1kIHdkamdkYiB0b3dzZ2RmIHRic2Vnb2IuIE9ZQXQgbXNiIG0gZnNibXkgbG11IHl3IGpibXNkIG0gbGdyYiBtc3NtdSB3YSBvd3pwa3licyB0Ym9rc2d5dSB0cWdqanQgZ2QgbSB0bWFiLCBqYmZtaiBiZGVnc3dkemJkeSwgbWRyIG1zYiB4d3R5YnIgbWRyIHBqbXViciBodSB6bWR1IHRib2tzZ3l1IGZzd2twdCBtc3drZHIgeXhiIGx3c2pyIGF3cyBha2QgbWRyIHBzbW95Z29iLiBBd3MgeXhndCBwc3doamJ6LCB5eGIgYWptZiBndDogcGdvd09ZQXtBUzNDSzNET1VfNDc3NE9RNV80UzNfTzAwMV82QjA2NTlBSH0).

```text
CTFs (short for capture the flag) are a type of computer security competition. Contestants are presented with a set of challenges which test their creativity, technical (and googling) skills, and problem-solving ability. Challenges usually cover a number of categories, and when solved, each yields a string (called a flag) which is submitted to an online scoring service. CTFs are a great way to learn a wide array of computer security skills in a safe, legal environment, and are hosted and played by many security groups around the world for fun and practice. For this problem, the flag is: picoCTF{FR3QU3NCY_4774CK5_4R3_C001_6E0659FB}
```

Flag: `picoCTF{FR3QU3NCY_4774CK5_4R3_C001_6E0659FB}`

<br>

### substitution2
`100 points` `3471 solves`

> `Substitution`<br>
> It seems that another encrypted message has been intercepted. The encryptor seems to have learned their lesson though and now there isn't any punctuation! Can you still crack the cipher?
> 
> ```text
> tzvwvvfsotovmvwrpktzvwcvppvotrlpsozvyzshzoizkkpikqgntvwovinwstjikqgvtstskeoseipnysehijlvwgrtwsktreynoijlvwizrppvehvtzvovikqgvtstskeoxkinogwsqrwspjkeojotvqoryqsesotwrtskexneyrqvetrpoczsizrwvmvwjnovxnpreyqrwuvtrlpvousppozkcvmvwcvlvpsvmvtzvgwkgvwgnwgkovkxrzshzoizkkpikqgntvwovinwstjikqgvtstskesoektkepjtktvrizmrpnrlpvousppolntrpoktkhvtotnyvetosetvwvotvysereyvfistvyrlkntikqgntvwoisveivyvxveosmvikqgvtstskeorwvkxtveprlkwsknorxxrsworeyikqvykcetkwneesehizviupsotoreyvfvintsehikexshoiwsgtokxxveovketzvktzvwzreysozvrmspjxkinovykevfgpkwrtskereysqgwkmsortskereykxtvezrovpvqvetokxgprjcvlvpsvmvrikqgvtstsketknizsehketzvkxxveosmvvpvqvetokxikqgntvwovinwstjsotzvwvxkwvrlvttvwmvzsipvxkwtvizvmrehvpsoqtkotnyvetoserqvwsirezshzoizkkpoxnwtzvwcvlvpsvmvtzrtreneyvwotreysehkxkxxveosmvtvizesanvosovoovetsrpxkwqknetsehrevxxvitsmvyvxveovreytzrttzvtkkporeyikexshnwrtskexkinoveiknetvwvyseyvxveosmvikqgvtstskeoykvoektpvryotnyvetotkuekctzvswvevqjrovxxvitsmvpjrotvrizsehtzvqtkritsmvpjtzseupsuvrerttriuvwgsikitxsorekxxveosmvpjkwsvetvyzshzoizkkpikqgntvwovinwstjikqgvtstsketzrtovvuotkhvevwrtvsetvwvotseikqgntvwoisveivrqkehzshzoizkkpvwotvrizsehtzvqveknhzrlkntikqgntvwovinwstjtkgsanvtzvswinwskostjqktsmrtsehtzvqtkvfgpkwvketzvswkcereyverlpsehtzvqtklvttvwyvxveytzvswqrizsevotzvxprhsogsikITX{E6W4Q_4E41J515_15_73Y10N5_42VR1770}
> ```

Same as above, harder as there are no spaces but it was possible. The message was decoded successfully using [CyberChef](https://gchq.github.io/CyberChef/#recipe=Substitute('rliyvxhzsupqekgawotnmcfjITXEWQJYNVR','abcdefghiklmnopqrstuvwxyCTFNRMYDUEA')&input=dHp2d3Z2ZnNvdG92bXZ3cnBrdHp2d2N2cHB2b3RybHBzb3p2eXpzaHpvaXpra3Bpa3FnbnR2d292aW53c3RqaWtxZ3Z0c3Rza2Vvc2VpcG55c2VoaWpsdndncnR3c2t0cmV5bm9pamx2d2l6cnBwdmVodnR6dm92aWtxZ3Z0c3Rza2VveGtpbm9nd3NxcndzcGprZW9qb3R2cW9yeXFzZXNvdHdydHNrZXhuZXlycXZldHJwb2N6c2l6cnd2bXZ3am5vdnhucHJleXFyd3V2dHJscHZvdXNwcG96a2N2bXZ3Y3ZsdnBzdm12dHp2Z3drZ3Z3Z253Z2tvdmt4cnpzaHpvaXpra3Bpa3FnbnR2d292aW53c3RqaWtxZ3Z0c3Rza2Vzb2VrdGtlcGp0a3R2cml6bXJwbnJscHZvdXNwcG9sbnRycG9rdGtodnRvdG55dmV0b3NldHZ3dm90dnlzZXJleXZmaXN0dnlybGtudGlrcWdudHZ3b2lzdmVpdnl2eHZlb3NtdmlrcWd2dHN0c2tlb3J3dmt4dHZlcHJsa3dza25vcnh4cnN3b3JleWlrcXZ5a2NldGt3bmVlc2VoaXp2aXVwc290b3JleXZmdmludHNlaGlrZXhzaG9pd3NndG9reHh2ZW92a2V0enZrdHp2d3pyZXlzb3p2cm1zcGp4a2lub3Z5a2V2Zmdwa3dydHNrZXJleXNxZ3drbXNvcnRza2VyZXlreHR2ZXpyb3ZwdnF2ZXRva3hncHJqY3ZsdnBzdm12cmlrcWd2dHN0c2tldGtuaXpzZWhrZXR6dmt4eHZlb3NtdnZwdnF2ZXRva3hpa3FnbnR2d292aW53c3Rqc290enZ3dnhrd3ZybHZ0dHZ3bXZ6c2lwdnhrd3R2aXp2bXJlaHZwc29xdGtvdG55dmV0b3NlcnF2d3NpcmV6c2h6b2l6a2twb3hud3R6dndjdmx2cHN2bXZ0enJ0cmVuZXl2d290cmV5c2Voa3hreHh2ZW9zbXZ0dml6ZXNhbnZvc292b292ZXRzcnB4a3dxa25ldHNlaHJldnh4dml0c212eXZ4dmVvdnJleXR6cnR0enZ0a2twb3JleWlrZXhzaG53cnRza2V4a2lub3ZlaWtuZXR2d3Z5c2V5dnh2ZW9zbXZpa3FndnRzdHNrZW95a3ZvZWt0cHZyeW90bnl2ZXRvdGt1ZWtjdHp2c3d2ZXZxanJvdnh4dml0c212cGpyb3R2cml6c2VodHp2cXRrcml0c212cGp0enNldXBzdXZyZXJ0dHJpdXZ3Z3Npa2l0eHNvcmVreHh2ZW9zbXZwamt3c3ZldHZ5enNoem9pemtrcGlrcWdudHZ3b3ZpbndzdGppa3FndnRzdHNrZXR6cnRvdnZ1b3RraHZldndydHZzZXR2d3ZvdHNlaWtxZ250dndvaXN2ZWl2cnFrZWh6c2h6b2l6a2twdndvdHZyaXpzZWh0enZxdmVrbmh6cmxrbnRpa3FnbnR2d292aW53c3RqdGtnc2FudnR6dnN3aW53c2tvc3RqcWt0c21ydHNlaHR6dnF0a3ZmZ3Brd3ZrZXR6dnN3a2NlcmV5dmVybHBzZWh0enZxdGtsdnR0dnd5dnh2ZXl0enZzd3FyaXpzZXZvdHp2eHByaHNvZ3Npa0lUWHtFNlc0UV80RTQxSjUxNV8xNV83M1kxME41XzQyVlIxNzcwfQ).

```text
thereexistseveralotherwellestablishedhighschoolcomputersecuritycompetitionsincludingcyberpatriotanduscyberchallengethesecompetitionsfocusprimarilyonsystemsadministrationfundamentalswhichareveryusefulandmarketableskillshoweverwebelievetheproperpurposeofahighschoolcomputersecuritycompetitionisnotonlytoteachvaluableskillsbutalsotogetstudentsinterestedinandexcitedaboutcomputersciencedefensivecompetitionsareoftenlaboriousaffairsandcomedowntorunningchecklistsandexecutingconfigscriptsoffenseontheotherhandisheavilyfocusedonexplorationandimprovisationandoftenhaselementsofplaywebelieveacompetitiontouchingontheoffensiveelementsofcomputersecurityisthereforeabettervehiclefortechevangelismtostudentsinamericanhighschoolsfurtherwebelievethatanunderstandingofoffensivetechniquesisessentialformountinganeffectivedefenseandthatthetoolsandconfigurationfocusencounteredindefensivecompetitionsdoesnotleadstudentstoknowtheirenemyaseffectivelyasteachingthemtoactivelythinklikeanattackerpicoctfisanoffensivelyorientedhighschoolcomputersecuritycompetitionthatseekstogenerateinterestincomputerscienceamonghighschoolersteachingthemenoughaboutcomputersecuritytopiquetheircuriositymotivatingthemtoexploreontheirownandenablingthemtobetterdefendtheirmachinestheflagispicoCTF{N6R4M_4N41Y515_15_73D10U5_42EA1770}
```

Flag: `picoCTF{N6R4M_4N41Y515_15_73D10U5_42EA1770}`

<br>

### transposition-trial
`100 points` `3244 solves`

> Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.
> 
> ```text
> heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V9AAB1F8}7
> ```

View the message as blocks of 3 characters, the last character of the block should be the first character. Rearrange the order accordingly to obtain the flag.

```python
msg = "heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V9AAB1F8}7"
flag = ""

for i in range(0, len(msg), 3):
    flag += msg[i+2] + msg[i:i+2]

print(flag)
```

Flag: `picoCTF{7R4N5P051N6_15_3XP3N51V3_A9AFB178}`

<br>

### Vigenere
`100 points` `4656 solves`

> Can you decrypt this message?<br>
> Decrypt this message using this key "CYLAB".
> 
> ```text
> rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_2951c89f}
> ```

The provided key was used to decrypt the flag using [CyberChef](https://gchq.github.io/CyberChef/#recipe=Vigen%C3%A8re_Decode('CYLAB')&input=cmdub0RWRHtPME5VX1dRM19HMUczTzNUM19BMUFIM1NfMjk1MWM4OWZ9Cg).

Flag: `picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_2951a89h}`

<br>

### diffie-hellman
`200 points` `2572 solves`

> Alice and Bob wanted to exchange information secretly. The two of them agreed to use the Diffie-Hellman key exchange algorithm, using p = 13 and g = 5. They both chose numbers secretly where Alice chose 7 and Bob chose 3. Then, Alice sent Bob some encoded text (with both letters and digits) using the generated key as the shift amount for a Caesar cipher over the alphabet and the decimal digits. Can you figure out the contents of the message?
> 
> ```text
> H98A9W_H6UM8W_6A_9_D6C_5ZCI9C8I_8F7GK99J
> ```
> 
> Wrap your decrypted message in the picoCTF flag format like  `picoCTF{decrypted_message}`

The public key was calculated by `B = g^b mod p = 5^3 mod 13 = 8`, which was then used to calculate the private key by `B^a mod p = 8^7 mod 13 = 5`.

The message was decrypted as caesar cipher that shifts it by 5 place using [https://www.dcode.fr/caesar-cipher](https://www.dcode.fr/caesar-cipher).

Flag: `picoCTF{C4354R_C1PH3R_15_4_817_0U7D473D_3A2BF44E}`

<br>
