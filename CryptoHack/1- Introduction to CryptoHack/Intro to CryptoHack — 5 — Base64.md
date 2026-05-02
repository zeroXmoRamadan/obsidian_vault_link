> **Source:** CryptoHack — Introductory Challenge
> **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#encoding` `#base64`

## What is This Challenge?

**Base64** is an encoding scheme that represents binary data as an ASCII string using an alphabet of 64 characters (`A–Z`, `a–z`, `0–9`, `+`, `/`).

- 1 Base64 character = **6 bits**
- 4 Base64 characters = **3 bytes** (24 bits)

It's widely used on the web to embed binary data (images, files) inside HTML/CSS/JSON — anywhere only text is safe to transmit.

This challenge asks you to decode a hex string into bytes, then re-encode those bytes as Base64.

## What To Do

Given hex string:

```
72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf
```

Solve with Python:

```python
import base64

hex_string = "72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf"
raw_bytes = bytes.fromhex(hex_string)
print(base64.b64encode(raw_bytes).decode())
```

## Flag

![](Pasted%20image%2020260502174020.png)

```bash
crypto/Base+64+Encoding+is+Web+Safe/
```

## How It Works

1. `bytes.fromhex()` converts the hex string → raw bytes
2. `base64.b64encode()` encodes those bytes → Base64 bytes
3. `.decode()` converts the Base64 bytes → a readable string

## Key Takeaways

- Base64 is **not** encryption — it's just an encoding format
- Hex → Bytes → Base64 is a common conversion chain in CTFs
- Base64 strings often end with `=` or `==` padding
- Spotting Base64: long strings of alphanumeric chars ending in `=`
- `base64.b64decode()` reverses the process

## Resources

- [Wikipedia: Base64](https://en.wikipedia.org/wiki/Base64)
- [ASCII Table](https://www.rapidtables.com/code/text/ascii-table.html)