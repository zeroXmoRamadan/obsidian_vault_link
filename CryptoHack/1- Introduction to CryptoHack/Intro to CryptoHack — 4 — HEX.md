> **Source:** CryptoHack — Introductory Challenge
> **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#encoding` `#hex`

## What is This Challenge?

Encrypted data often contains **non-printable bytes** that can't be safely shared as plain text. **Hexadecimal (base-16)** is a common way to encode such data into a portable, human-readable format.

The encoding process:

1. Each character → ASCII ordinal (decimal)
2. Decimal → base-16 (hex)
3. All hex values concatenated into one long string

This challenge gives you a hex string and asks you to decode it back into readable text.

## What To Do

Given hex string:

```
63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d
```

Decode it with Python:

```python
print(bytes.fromhex("63727970746f7b596f755f77696c6c5f62655f776f726b696e675f776974685f6865785f737472696e67735f615f6c6f747d").decode())
```

## Flag

![](Pasted%20image%2020260502173727.png)

```
crypto{You_will_be_working_with_hex_strings_a_lot}
```

## How It Works

- `bytes.fromhex(hex_string)` converts a hex string → raw bytes
- `.decode()` interprets those bytes as a UTF-8/ASCII string
- The reverse: `"hello".encode().hex()` gives you the hex representation

## Key Takeaways

- Hex encoding is **not** encryption — it's just a representation format
- Two hex characters = one byte (e.g. `63` → `99` → `'c'`)
- `bytes.fromhex()` and `.hex()` are your go-to Python tools for hex challenges
- You'll see hex constantly in CTFs — for ciphertexts, keys, IVs, and hashes

## Resources

- [ASCII Table](https://www.rapidtables.com/code/text/ascii-table.html)
- [Wikipedia: Hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal)