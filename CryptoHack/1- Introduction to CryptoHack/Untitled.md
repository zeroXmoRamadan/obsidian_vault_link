> **Source:** CryptoHack — Introductory Challenge **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#xor` `#bitwise`

## What is This Challenge?

**XOR** (exclusive OR) is a fundamental bitwise operation in cryptography. It returns `0` if both bits are the same, and `1` if they differ.

|A|B|Output|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

For multi-bit values, XOR is applied **bit by bit**:

```
0110 ^ 1010 = 1100
```

For strings, each character is first converted to its Unicode integer, XOR'd, then converted back.

This challenge asks you to XOR each character of `"label"` with the integer `13`.

## What To Do

```python
plaintext = "label"
key = 13

result = "".join(chr(ord(c) ^ key) for c in plaintext)
print(f"crypto{{{result}}}")
```

## Flag

```
crypto{aloha}
```

## How It Works

- `ord(c)` converts each character to its Unicode integer
- `^ 13` XORs that integer with the key
- `chr()` converts the result back to a character
- The characters are joined and wrapped in `crypto{}`

## Key Takeaways

- XOR is **symmetric**: `a ^ k = b` and `b ^ k = a` — the same operation encrypts and decrypts
- XOR with `0` returns the original value: `a ^ 0 = a`
- XOR with itself returns zero: `a ^ a = 0`
- These properties make XOR the backbone of stream ciphers and one-time pads
- `pwntools` `xor()` handles mixed types and lengths — useful for more complex challenges

## Resources

- [pwntools docs – xor()](https://docs.pwntools.com/en/stable/util/fiddling.html#pwnlib.util.fiddling.xor)