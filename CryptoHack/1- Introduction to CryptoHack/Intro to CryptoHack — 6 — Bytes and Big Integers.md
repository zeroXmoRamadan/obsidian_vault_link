> **Source:** CryptoHack — Introductory Challenge
> **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#encoding` `#rsa` `#pycryptodome`

## What is This Challenge?

Cryptosystems like **RSA** operate on **numbers**, but messages are made of characters. The standard way to bridge this gap:

1. Take each character's ASCII ordinal byte
2. Convert to hex
3. Concatenate all hex values → one big hex number
4. Interpret as base-16, which can also be expressed in base-10

**Example:**

|Step|Value|
|---|---|
|Message|`HELLO`|
|ASCII bytes|`[72, 69, 76, 76, 79]`|
|Hex bytes|`[0x48, 0x45, 0x4c, 0x4c, 0x4f]`|
|Base-16|`0x48454c4c4f`|
|Base-10|`310400273487`|

This challenge gives you a large integer and asks you to convert it back into a readable message.

## What To Do

Given integer:

```
11515195063862318899931685488813747395775516287289682636499965282714637259206269
```

Solve with Python:

```python
from Crypto.Util.number import long_to_bytes

n = 11515195063862318899931685488813747395775516287289682636499965282714637259206269
print(long_to_bytes(n).decode())
```

> Install PyCryptodome first if needed:
> 
> ```bash
> pip install pycryptodome
> ```

## Flag

![](Images/Pasted%20image%2020260502174333.png)

```
crypto{3nc0d1n6_4ll_7h3_w4y_d0wn}
```

## How It Works

- `long_to_bytes(n)` converts a big integer → raw bytes (reversing the hex concatenation)
- `.decode()` interprets those bytes as a readable ASCII string
- The reverse: `bytes_to_long(b"HELLO")` converts bytes → integer

## Key Takeaways

- RSA and other math-based cryptosystems require messages to be integers — this conversion is how it's done
- `bytes_to_long()` / `long_to_bytes()` from `Crypto.Util.number` are essential RSA tools
- The bigger the message, the bigger the integer — RSA key size must exceed the message size
- This encoding is **lossless** — you can always recover the original message

## Resources

- [PyCryptodome Docs](https://pycryptodome.readthedocs.io/)
- [CryptoHack FAQ – Installing PyCryptodome](https://cryptohack.org/faq/#install)
