> **Source:** CryptoHack — Introductory Challenge **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#xor` `#known-plaintext`

## What is This Challenge?

A flag has been encrypted with a **repeating-key XOR** cipher. The key length is unknown, but the flag format `crypto{` gives us a **known plaintext crib** — we can XOR the ciphertext against what we know the plaintext starts with to recover the key.

## Given Data

```
0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104
```

## Solution

```python
from pwn import xor

ciphertext = bytes.fromhex("0e0b213f26041e480b26217f27342e175d0e070a3c5b103e2526217f27342e175d0e077e263451150104")

# XOR known plaintext prefix against ciphertext to extract the key
known = b"crypto{"
key = xor(ciphertext[:len(known)], known)
print(f"Partial key: {key}")  # reveals the key pattern

# The key repeats — extend it to decrypt the full ciphertext
full_key = (key * (len(ciphertext) // len(key) + 1))[:len(ciphertext)]
flag = xor(ciphertext, full_key)
print(flag.decode())
```

### Or using CyberChef
1. ![](Pasted%20image%2020260502180409.png)
2. ![](Pasted%20image%2020260502180438.png)
## Flag

```
crypto{1f_y0u_Kn0w_En0uGH_y0u_Kn0w_1t_4ll}
```

## How It Works

1. We know the flag starts with `crypto{` — that's 7 bytes of known plaintext
2. XOR the first 7 bytes of ciphertext with `crypto{` → reveals the first 7 bytes of the key
3. The key repeats — use it to decrypt the entire ciphertext

This works because of the XOR self-inverse property:

```
ciphertext = plaintext ^ key
ciphertext ^ plaintext = key
```

## Key Takeaways

- **Known-plaintext attack**: if you know any part of the plaintext, you can recover that portion of the key
- Flag formats like `crypto{` are intentional cribs — always try XORing them against the start of ciphertext
- Repeating-key XOR is weak: once you know the key length, each byte position is just single-byte XOR
- This is the core idea behind breaking **Vigenère cipher** and basic stream ciphers