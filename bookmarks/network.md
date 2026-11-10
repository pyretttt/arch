[[computer-networking-top-down-approach-9th.pdf#page=440&selection=53,0,53,46|Because there are both network-layer addresses]]

# Cryptography
***
[[network-security-private-3rd.pdf#page=127&selection=72,0,72,70|What can an attacker do if he can find two messages with the same hash]]


## 4-6-Homework
***
1. [[network-security-private-3rd.pdf#page=123&selection=54,0,73,19|In our example mode Randomized ECB (see Figure 4-4), suppose that a bit of one of the ciphertext blocks, say ci, is flipped (intentionally or unintentionally). What will that do to the decrypted message? Suppose a bit of an r i is flipped? What would that do to the decrypted message? Suppose the ciphertext were being transmitted as a stream of octets, and one octet was lost (and the receiver was not notified that an octet was lost)? What would that do to the decrypted message?]]

- It will result in arbitrary $m_{i}$ block, other blocks won't be affected $r_{i}$ will stay the same. 
- If one bit of $r_{i}$ is flipped one bit of $m_{i}$ will be wrong
- If one octets is lost, then decryption payload shifts by 8 bits. All consequent blocks will be decrypted incorrectly. 

1. [[network-security-private-3rd.pdf#page=124&selection=9,0,13,18|In CBC mode, suppose one bit of ciphertext is flipped. What will that do to the decrypted message? Suppose the ciphertext were being transmitted as a stream of octets, and one octet was lost (without the receiver being notified that an octet was lost)? What would that do to the decrypted message? Suppose an entire block was lost. What would that do to the decrypted message?]]

- If $c_{i}$ is flipped then $m_{i}$ will be arbitrary and $m_{i + 1}$ will contain one bit flipped
- If one octet is lost, then every consequent block will be decrypted incorrectly
- If entire block is lost then block after the lost one receives incorrect random number instead of $r_{i}$ it will receive $r_{i - 1}$. The random vector that was not used during encryption, so that decryption of this one block will fail. So that $m_{i + 1}$ is garbled all the other are fine.

1. [[network-security-private-3rd.pdf#page=124&selection=16,0,22,88|Consider the following alternative method of encrypting a message. To encrypt a message, use the algorithm for CBC decryption with an implicit IV of zero. To decrypt a message, use the algorithm for CBC encryption with an implicit IV of zero. Would this work? (“Working” means that decrypt reverses the encrypt operation.) What are the security implications of this, if any, as contrasted with the “normal” CBC? Hints: How many ciphertext blocks change if you change one block of message in normal CBC compared to our proposed CBC variant? If there are repeated blocks of plaintext, are there detectable patterns in the ciphertext?]]

- Will this even work? Let's check
$Enc(m_{i}) = D(m_{i}) \otimes m_{i - 1}$ And $Dec(c_{i}) = E(c_{i} \otimes m_{i - 1})$ then we have

$$\begin{align}
Dec(Enc(m_{i})) = E(D(m_{i}) \otimes m_{i -1} \otimes m_{i - 1}) \\
= E(D(m_{i})) = m_{i}
\end{align}$$
So yes it will work

- How many ciphertext blocks change if you change one block of message in normal CBC compared to proposed CBC variant

If we change one block of message in normal CBC all consequent blocks will be changed

In proposed variant only one changed block and one consequent block will be changed

- If there's a 3 repeated blocks only first one will be encrypted meaningfully, the other two will be the same. So some information leaks.

4. [[network-security-private-3rd.pdf#page=124&selection=25,0,33,35|Suppose you know that the employee database is encrypted using randomized ECB (see §4.2.2.1), and suppose you know that your salary is in plaintext block m7 , that you have access to the ciphertext, and you know the syntax of the plaintext. How can you modify the ciphertext to increase your salary?]]

As soon as $Enc(m_{7}, r_{7}) = E(m_{7} \otimes r_{7})$ and decryption is $Dec(c_{7}, r_{7}) = D(c_{7}) \otimes r_{7}$ where $D(c_{7}) = m_{7} \otimes r_{7}$. So that if encryption keeps initial $r_{7}$, but decryption uses altered $r_{7}'$ we have $Dec(c_{7}, r_{7}') = D(c_{7}) \otimes r_{7}' = m_{7} \otimes r_{7} \otimes r_{7}'$. Then by changing $r_{7}'$ we can get predictable result for encryption.

5. [[network-security-private-3rd.pdf#page=124&selection=36,0,37,88|Why is it possible to decrypt, in parallel, blocks of ciphertext that were encrypted using CBC mode, but it is not possible to encrypt, in parallel, blocks of plaintext with CBC mode?]]

- It's possible to decrypt in parallel because the input of the decryption function does not depend on previous calculations - $Dec(c_{i}) = D(c_{i}) \otimes c_{i - 1}$ where $c_{0} = IV$. All the inputs are ready at the start of decryption
- It's not possible to encrypt CBC mode in parallel because encryption function depends on calculations of the previous block - $Enc(m_{i}) = E(m_{i} \otimes c_{i - 1})$, with $c_{0} = IV$ i.e. we don't know $c_{i - 1}$ for all blocks.

6. [[network-security-private-3rd.pdf#page=124&selection=40,0,47,29|Suppose a message is encrypted with CTR mode, and you know that plaintext block m7 contains your salary. Suppose you have access to the ciphertext. How can you modify the ciphertext to increase your salary?]]

- To Decrypt with Counter mode we do two things: (1) extract encrypted $IV$ as $K(IV + 6, K) = c_{7} \otimes m_{7}$ and thereof $m_{7} = c_{7} \otimes E(IV + 6, K)$. Once we know the $m_{7}$ is $XOR$ between $c_{7}$ and $E(IV + 6, K)$ - we can change $c_{7}$ in predictable way to obtain arbitrary $m_{7}'$

7. [[network-security-private-3rd.pdf#page=124&selection=50,0,51,13|In CBC mode, suppose you reused the same IV for two messages. What are the security implications?]]

- Sending same IV leaks data about repetitive information which rarely changes. For example once something changes eavesdropper - can say that something really changed. Changing $IV$ each time guarantees that even the same plaintext will be different each time

8. [[network-security-private-3rd.pdf#page=124&selection=54,0,60,75|Suppose you wanted to decrypt only block n of a file that was encrypted with CBC mode (and you knew the key with which the file was encrypted). Which blocks of the encrypted file would you need to read? What cryptographic operations would you need to do?]]

- To decrypt only block $n$ of file with known secret key, I would also need block encrypted block $n - 1$. Required operation is $m_{n} = D(c_{n}, K) \otimes c_{n - 1}$ where $c_{0} = IV$

9. [[network-security-private-3rd.pdf#page=124&selection=63,0,75,1|How does ⊕ing K1 into the final block in CMAC prevent the attack described in section §4.3.1.1 CBC Forgery Attack?]]

> Because any intermediate value for instance tag of $m_{1}|m_{2}|m_{3}$, won't be the same value that is XORed from the same prefix in $(m_{1}|m_{2}|m_{3})|m_{4}|m_{5}|m_{6}$. So that tag of $CMAC(CMAC(m_{1} | m_{2} | m_{3}) \otimes m_{4}|m_{5}|m_{6})$ won't be equal to $CMAC(m_{1}|m_{2}|m_{3}|m_{4}|m_{5}|m_{6})$


10. [[network-security-private-3rd.pdf#page=124&selection=76,4,103,24|For each scenario, compare the number of AES operations required in XTS versus XEX: a) Encrypting an n-block plaintext that is an integral number of blocks. b) Encrypting an n-block plaintext that is not an integral number of blocks. c) Decrypting an n-block ciphertext. d) Decrypting only block n. (Two questions: if the ciphertext is an integral number of blocks, or if it isn’t.) e) Decrypting only block n−1. (Two questions: if the ciphertext is an integral number of blocks, or if it isn’t.)]]

- (a) Encrypting an $n$ - block plaintext that is an integral number of blocks

$n + 1$ one for $IV$ encryption and $n$ for $n$ blocks

- (b) Encrypting an $n$ - block plaintext that is not an integral number of blocks

XEX do not support partial blocks, XTS $n + 1$

- (c) Decrypt \(n\) full blocks (c-2) Decrypt \(n\) blocks, last partial

$n + 1$ for both algorithms if blocks are full. XEX do not support partial blocks, XTS $n + 1$ if blocks are partial

- (d) Decrypt only block $n - 1$

2 operation one for $IV$ and one for block. If last is partial XTS requires 3 operations 

- (e) Decrypt only block \(n-1\)

2 operation one for $IV$ and one for block. If last is partial XTS requires 3 operations 

- (f) Decrypt only block \(n-2\), all full

Two operations if blocks are full, not supported for XEX if blocks are partial

11. [[network-security-private-3rd.pdf#page=125&selection=19,4,20,18|How can you do an XTS-like trick with CBC mode encryption (and decryption) so as to be length-preserving?]]

Encrypt:

```
m4   |m5|     |
|        |  /
XOR    XOR /  
|    /   |/
E   /   /E 
|  /   / |
 -----   c4
|  |  | / 
 ----- / 
   \  /  
    \/
   / \
 c4    c5
```

Decrypt:
```
c4       c5
|        |
D   |     |  |  
|   /     |
XOR       D
|         |
|m5| |   XOR <---- c3
   \   / 
	\ / 
     /\
    /  \
  m4    m5
```

12. [[network-security-private-3rd.pdf#page=125&selection=21,4,57,1|What message could you forge (see section §4.3.1.1 CBC Forgery Attack) if you saw two messages with CBC-MACs—one that consisted of m1|m2 with CBC-MAC x1, and another that consisted of m1|m2|m3|m4 with CBC-MAC x2?]]

`CBCMAC(m1|m2) = x1` then we can forge like that `m1|m2|(m1 XOR x1)|m2|m3|m4` will also result in `x2`

13. [[network-security-private-3rd.pdf#page=125&selection=58,4,136,5|With CBC-MAC, it is possible to create a message that has all but one block chosen by the user and has any chosen CBC-MAC value, provided that one block somewhere in the message is constrained by the computation rather than chosen by the user. Show how you can construct a message that has CBC-MAC equal to 0, where you want particular values for m1 , m2, m3, m4 , m6 , m7 , m8 , and you don’t care what value is in m5 . You can do this with any key, so let’s say you are constrained to use key=K, and let’s say you are using AES-128. What does m5 need to be so that the message m1|m2|m3|m4|m5|m6|m7|m8 will have CBC-MAC equal to 0?]]

**Setup.** CBC-MAC with IV = 0 and key K:

- c0 = 0
- ci = E_K(m_i ⊕ c_{i-1}) for i = 1..8
- MAC = c8

**Goal:** c8 = 0, with m1, m2, m3, m4, m6, m7, m8 chosen freely and m5 forced.

**Idea:** Work forward from the start and backward from the end, then make the two meet at block 5. The forward direction needs only encryption. The backward direction uses decryption, which is fine because we know K.

**Step 1: forward from the start.** Compute

- c1 = E_K(m1)
- c2 = E_K(m2 ⊕ c1)
- c3 = E_K(m3 ⊕ c2)
- c4 = E_K(m4 ⊕ c3)

c4 depends only on m1..m4, so it is known.

**Step 2: backward from the end.** We need c8 = 0, so

- c8 = 0 = E_K(m8 ⊕ c7), so c7 = D_K(0) ⊕ m8
- c7 = E_K(m7 ⊕ c6), so c6 = D_K(c7) ⊕ m7
- c6 = E_K(m6 ⊕ c5), so c5 = D_K(c6) ⊕ m6

So c5 is determined by m6, m7, m8 and K:

c5 = D_K( D_K( D_K(0) ⊕ m8 ) ⊕ m7 ) ⊕ m6

**Step 3: solve for m5.** We need c5 = E_K(m5 ⊕ c4). Therefore

m5 ⊕ c4 = D_K(c5), so m5 = D_K(c5) ⊕ c4

**Final formula**

m5 = c4 ⊕ D_K( D_K( D_K( D_K(0) ⊕ m8 ) ⊕ m7 ) ⊕ m6 ⊕ 0 ) ...

Written cleanly, with the intermediate values:

- c4 = E_K(m4 ⊕ E_K(m3 ⊕ E_K(m2 ⊕ E_K(m1))))
- c5 = D_K( D_K( D_K(0) ⊕ m8 ) ⊕ m7 ) ⊕ m6
- **m5 = D_K(c5) ⊕ c4**

**Verification.** With this m5, E_K(m5 ⊕ c4) = E_K(D_K(c5)) = c5. Then c6 = E_K(m6 ⊕ c5) = E_K(D_K(c6)) = c6 as constructed. Similarly c7 follows, and c8 = E_K(m8 ⊕ c7) = E_K(D_K(0)) = 0. So the MAC is 0.