> **Source:** CryptoHack — Introductory Challenge
> **Tags:** `#ctf` `#cryptohack` `#cryptography` `#python` `#xor` `#bitwise`

## What is This Challenge?

This challenge covers the four core **properties of XOR** and asks you to use them to undo a chain of XOR encryptions to recover a flag.

### XOR Properties

|Property|Rule|
|---|---|
|**Commutative**|`A ⊕ B = B ⊕ A`|
|**Associative**|`A ⊕ (B ⊕ C) = (A ⊕ B) ⊕ C`|
|**Identity**|`A ⊕ 0 = A`|
|**Self-Inverse**|`A ⊕ A = 0`|

## Given Data

```
KEY1                    = a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313
KEY2 ^ KEY1             = 37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e
KEY2 ^ KEY3             = c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1
FLAG ^ KEY1 ^ KEY3 ^ KEY2 = 04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf
```

## Solution

The goal is to isolate `FLAG`. Starting from:

```
FLAG ^ KEY1 ^ KEY2 ^ KEY3
```

XOR it with `KEY1`, `KEY2`, and `KEY3` to cancel them out (self-inverse property).

We don't have `KEY2` or `KEY3` directly, but we can derive them:

- `KEY2 = (KEY2 ^ KEY1) ^ KEY1`
- `KEY3 = (KEY2 ^ KEY3) ^ KEY2`

Then: `FLAG = (FLAG ^ KEY1 ^ KEY2 ^ KEY3) ^ KEY1 ^ KEY2 ^ KEY3`

```python
from pwn import xor

KEY1         = bytes.fromhex("a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313")
KEY2_KEY1    = bytes.fromhex("37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e")
KEY2_KEY3    = bytes.fromhex("c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1")
FLAG_enc     = bytes.fromhex("04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf")

KEY2 = xor(KEY2_KEY1, KEY1)
KEY3 = xor(KEY2_KEY3, KEY2)
FLAG = xor(FLAG_enc, KEY1, KEY2, KEY3)

print(FLAG.decode())
```

## Flag

![](Images/Pasted%20image%2020260502175417.png)

```
crypto{x0r_i5_ass0c1at1v3}
```

## How It Works

1. Recover `KEY2` by XORing `(KEY2 ^ KEY1)` with `KEY1` — the `KEY1` cancels out
2. Recover `KEY3` by XORing `(KEY2 ^ KEY3)` with `KEY2` — the `KEY2` cancels out
3. XOR the encrypted flag with all three keys — each cancels itself out, leaving only `FLAG`

## Key Takeaways

- The **associative + self-inverse** properties mean you can cancel any key by XORing it again
- You don't need all keys directly — you can **derive** them from XOR relationships
- This pattern (undoing XOR chains) appears constantly in block cipher and stream cipher attacks
- Always decode hex to bytes **before** XORing — operating on hex strings gives wrong results
