> **Source:** CryptoHack — Introductory Challenge
> **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#xor` `#brute-force`

## What is This Challenge?

A message has been XOR'd with a **single secret byte** (0–255). The key is unknown, but since there are only 256 possible values, we can try all of them — this is called a **brute-force** attack.

The flag format `crypto{...}` gives us a known plaintext crib to verify the correct key.

## Given Data

```
73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d
```

## Solution

```python
ciphertext = bytes.fromhex("73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d")

for key in range(256):
    decrypted = bytes([b ^ key for b in ciphertext])
    if decrypted.startswith(b"crypto{"):
        print(f"Key: {key}")
        print(decrypted.decode())
        break
```

### Using pwntools xor()

```Python
from pwn import xor

ciphertext = bytes.fromhex("73626960647f6b206821204f21254f7d694f7624662065622127234f726927756d")

for key in range(256):
    decrypted = xor(ciphertext, key)
    if decrypted.startswith(b"crypto{"):
        print(f"Key: {key}")
        print(decrypted.decode())
        break
```
## Flag

![](Images/Pasted%20image%2020260502175700.png)

```
crypto{0x10_15_my_f4v0ur173_by7e}
```

## How It Works

- Iterate over all 256 possible single-byte key values (`0x00` to `0xff`)
- XOR every byte of the ciphertext with the candidate key
- Check if the result starts with `crypto{` — if so, we found the key
- The correct key is `0x10` (decimal `16`)

## Key Takeaways

- **Single-byte XOR is trivially breakable** — only 256 keys to try
- Known plaintext (like a flag format) makes brute-force even faster — you only need to check the first few bytes
- This is the foundation of breaking **repeating-key XOR** (multi-byte keys), where each byte position is attacked independently
- Real stream ciphers need much larger key spaces to be secure
