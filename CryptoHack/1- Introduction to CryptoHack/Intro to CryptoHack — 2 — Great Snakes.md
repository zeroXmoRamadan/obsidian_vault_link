> **Source:** CryptoHack — Introductory Challenge
> **Tags:** #ctf #cryptohack #cryptography #python #intro

## What is This Challenge?

Modern cryptography relies on code — and that means knowing how to code. CryptoHack uses **Python 3** as the go-to language for writing cryptographic scripts and attacks due to its simplicity and powerful libraries.

This challenge introduces you to running Python scripts by executing an attached file that outputs a flag.

## What To Do

1. Download the challenge file: `great_snakes.py`
2. Make sure Python 3 is installed → [Download Python](https://wiki.python.org/moin/BeginnersGuide/Download)
3. Run the script:

```bash
python3 great_snakes.py
```

4. Copy the output flag and submit it

## Script Contents

```python
#!/usr/bin/env python3
import sys
# import this

if sys.version_info.major == 2:
    print("You are running Python 2, which is no longer supported. Please update to Python 3.")

ords = [81, 64, 75, 66, 70, 93, 73, 72, 1, 92, 109, 2, 84, 109, 66, 75, 70, 90, 2, 92, 79]

print("Here is your flag:")
print("".join(chr(o ^ 0x32) for o in ords))
```

## Flag

![](Pasted%20image%2020260502165716.png)

```bash
crypto{z3n_0f_pyth0n}
```

## How It Works

- `ords` is a list of integers
- Each integer is **XOR'd** with `0x32` (decimal `50`)
- `chr()` converts the result back to a character
- Joining all characters reveals the flag

This is a basic **XOR cipher** — one of the most fundamental operations in cryptography.

## Key Takeaways

- Python 3 is the standard language for CTF crypto challenges
- Running a `.py` script is as simple as `python3 filename.py`
- **XOR** (`^`) is a core crypto primitive: `value ^ key = ciphertext`, and `ciphertext ^ key = value`
- Some flags aren't hidden — they're revealed by simply running the right script