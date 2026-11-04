[[computer-networking-top-down-approach-9th.pdf#page=426&selection=6,0,6,48|Recall from our early discussion back in Section]]

# Cryptography
***

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

9. 