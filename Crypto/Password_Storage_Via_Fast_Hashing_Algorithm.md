/*
Title: Password Storage Uses Fast Hashing Algorithm
Description: Storing password hashes produced from fast hashing algorithms increases the odds of passwords being cracked.
*/

- LAST UPDATED DATE: 2015/12/2
- LAST UPDATED BY: @zaeyx

## Summary

Hashing algorithms are the defacto standard for disk resident password representation formats.  Such hashing algorithms are defined to only operate in one direction.  That is, they only turn plaintext passwords into their hashed form.  They cannot take a hash and "decrypt" it back into a plaintext password.  As such, an attacker attempting to reveal the plaintext associated with a hash has only one option, make brute force attempts at producing a matching hash.  Since hashing algorithms must also by definition be deterministic, if the attacker is able to find a hash which matches the hash he is attempting to "crack."  He can assume beyond all reasonable doubt that the plaintext he used to create that hash is the user's plaintet password.

The difference between "fast" and "slow" hashing algorithms is exactly that.  One algorithm takes very little time to compute.  The other takes much longer to compute, (is slow).

When dealing with fast hashing algorithms, and attacker is able to make many more guesses in the same amount of time, increasing his chance of finding the resulting plaintext password.

## Capabilities and Risk

Fast hashing algorithms are used primarily for their simplicity/ease of use, and speed/insignificant load on computational resources.  However when using fast hashing algorithms, you must understand that the passwords stored with this algorithm are potentially orders of magnitude easier to reveal to an attacker, should he gain access to the stored hashes.

With the plaintext passwords in hand, the attacker is highly likely to use the information to further his malicious intentions.  Or to leak the plaintext passwords on the internet in an attempt to embarrass and humiliate your service in the eyes of the public.

## Detection

Detection of such a vulnerability is exceedingly simple.  Determine if the algorithms your service uses to hash passwords is a fast or slow hashing algorithm (if it is a hashing algorithm at all).  

Examples of fast hashing algorithms are as follows:

	*[SHA-1](https://en.wikipedia.org/wiki/SHA-1)
	*[MD-5](https://en.wikipedia.org/wiki/MD5)
	*[SHA-2](https://en.wikipedia.org/wiki/SHA-2)
	*[LM](https://en.wikipedia.org/wiki/LM_hash)

If access to the application is limited for the purposes of ascertaining the the name of the algorithm used, it is often possible to determine the algorithm that generated a hash by looking at the hash itself.

One such tool capable of performing this analysis to a limited extent is John the Ripper, which can be found [here.](http://www.openwall.com/john/)

## Remediation

Remediation is simple.  One should upgrade any systems capable of receiving such an upgrade, to slow hashing algorithms. 

Examples of which are as follows: 

	*[BCrypt](https://en.wikipedia.org/wiki/Bcrypt)
	*[Crypt](https://en.wikipedia.org/wiki/Crypt_(C))
	*[PBKDF2](https://en.wikipedia.org/wiki/PBKDF2)

Another interesting hashing algorithm is [SCrypt](https://en.wikipedia.org/wiki/Scrypt) which uses extensive amounts of memory rather than time in order to limit an attacker's ability to parallel compute when attacking a hash.

If for some reason it is impossible for a system or service to be upgraded from a fast hashing algorithm, it is then paramount that a proper password policy be set and enforced in order to increase the complexity of stored passwords and increase the work the attacker must perform.

An example of a password policy that might mitigate the use of fast hashing algorithm to some extent is as follows:

	*Min-Length:21
	*Must Contain: Upper/Lower Alpha, Numeric, Special Char
	*Recommend: Passphrase, not password

## References

http://codahale.com/how-to-safely-store-a-password/
https://security.stackexchange.com/questions/4781/do-any-security-experts-recommend-bcrypt-for-password-storage
https://security.stackexchange.com/questions/15790/why-do-people-still-use-recommend-md5-if-it-is-cracked-since-1996
https://crackstation.net/hashing-security.htm

## Exploitation

Exploitation for an attacker is quite simple.  Just load an unknown hash that into a hash crackingg piece of software such as [John the Ripper](http://www.openwall.com/john/) and wait.  With a fast hashing algorithm and a bit of luck, it won't take long.
