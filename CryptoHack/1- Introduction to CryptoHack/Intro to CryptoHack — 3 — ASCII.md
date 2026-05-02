> **Source:** CryptoHack — Introductory Challenge
> **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#intro`

## What is This Challenge?

ASCII is a **7-bit encoding standard** that represents text using integers from `0` to `127`. Each number maps to a specific character — letters, digits, punctuation, and control codes.

This challenge gives you a list of integers and asks you to convert them into their corresponding ASCII characters to reveal a flag.

## What To Do

Given array:

```
[99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]
```

Run this Python one-liner:

```python
print("".join(chr(n) for n in [99, 114, 121, 112, 116, 111, 123, 65, 83, 67, 73, 73, 95, 112, 114, 49, 110, 116, 52, 98, 108, 51, 125]))
```

## Flag

![](Images/Pasted%20image%2020260502173316.png)

```
crypto{ASCII_pr1nt4bl3}
```

## How It Works

- Each integer in the array is an **ASCII code point**
- `chr(n)` converts an integer to its corresponding character
- `ord(c)` does the reverse — character back to integer
- Joining all characters reveals the flag

## Key Takeaways

- ASCII maps integers `0–127` to characters — memorizing the key ranges helps:
    - `65–90` → uppercase `A–Z`
    - `97–122` → lowercase `a–z`
    - `48–57` → digits `0–9`
- `chr()` and `ord()` are essential Python tools for encoding challenges
- Many CTF crypto problems are just encoding/decoding — not "real" encryption
