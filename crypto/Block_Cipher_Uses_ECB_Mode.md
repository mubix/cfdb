/*
Title: Block Cipher Uses ECB Mode
Description: A block cipher using ECB mode may reveal the contents of its ciphertext.
*/

- LAST UPDATED DATE: 2015/12/1
- LAST UPDATED BY: @zaeyx

## Summary

A block cipher in ECB mode encrypts every block of plaintext into ciphertext without using any additionaly nonce/input.  What this results in is that for every pair of matching plaintext inputs, their corresponding ciphertexts will also match.

## Capabilities and Risk

Though each block is still effectively encrypted to the specifications of the algorithm selected.  ECB mode does not do anything to change the output of a block to differentiate it from any other block if the two blocks are identical.  What this means in effect, is that if you encrypted the message "zaeyx is a cool dude, dude."  The "dude"s would come out as the same ciphertext.  The output might look something like "yuqbd jd q eadn defg, defg."  This reveals information about the plaintext.  And might in some cases be enough to allow the decryption of the entire message.  

## Detection

Detection of a block cipher operating in this mode can be accomplished by observing the output ciphertext for signs of repeating patterns equal to one block length.  With access to the cipher's implementation in code, one can check that ECB is or is not the mode of operation.

## Remediation

One must not operate block ciphers in ECB mode.  Switch to a preferred mode such at CTR (counter) mode, or CBC (cipher block chaining) among others.

## References

https://crypto.stackexchange.com/questions/20941/why-shouldnt-i-use-ecb-encryption
https://www.blackhat.com/presentations/bh-usa-06/BH-US-06-Eng.pdf
https://news.ycombinator.com/item?id=7959519

## Exploitation

An attacker may exploit a ciphertext encrypted in this manner by comparing blocks to find repeating patterns.  The attacker may then use this information to reveal the plaintext of the ciphertext by careful analysis.

