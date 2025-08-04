
# 🧠Introduction
Cryptography is foundational for securing communication online—it ensures your messages and data remain unreadable if intercepted 


# 🔐Types of Cryptography
Symmetric Encryption
Uses a single shared key for both encryption and decryption.
It’s fast but risky if the key is exposed, since anyone with the key can read messages 

Asymmetric Encryption
Uses two separate keys: a public key for encryption and a private key for decryption.
More secure, especially for high-stakes services like banking, because exposure of the public key doesn’t compromise decryption 

More secure? → Asymmetric,
Faster? → Symmetric,
Used by banks? → Asymmetric,
Public key? Used to encrypt messages,
Private key? Used to decrypt messages,
Does symmetric use two keys? → Nay 


# 🧩Hash Functions
A hash function takes any input and produces a fixed-size string; it's one-way—you can't reverse it.

Common uses: storing hashed passwords, verifying file integrity (e.g., matching hashes before and after download).

MD5: Stands for Message Digest 5, created by Ronald Rivest.

Example question: What's the MD5 hash of “hashes are cool”? → f762d32e3c160900d94b683e927555b9 


# 🔄Encoding vs. Encryption
Encoding
Transforms data into a different format (like Base64) that can be easily reversed without any secrets.

Example:
Encode “cryptographyisuseful” → Y3J5cHRvZ3JhcGh5aXN1c2VmdWw=
Decode “dGhlIHNlY3JldCB3b3JkIGlzIDogd2F0ZXJtZWxvbg==” → watermelon 


# ✅ Quick Q&A Recap
Question	-  Answer

Which is more secure: symmetric or asymmetric?	Asymmetric
Which is faster?	Symmetric
Which type will a bank site use?	Asymmetric
What key do you encrypt with in asymmetric cryptography?	Public key
What key do you decrypt with in asymmetric cryptography?	Private key
Does symmetric cryptography use two different keys?	No (Same key used both ways)
MD5 hash of “hashes are cool”?	f762d32e3c160900d94b683e927555b9
What does MD5 stand for?	Message Digest 5
Who created MD5?	Ronald Rivest
Base64 encode “cryptographyisuseful”?	Y3J5cHRvZ3JhcGh5aXN1c2VmdWw=
Base64 decode …? → “watermelon”	watermelon

# 🚀 Why These Concepts Matter
Symmetric cryptography is great for speed (e.g., encrypted files, secure tunnels).
Asymmetric cryptography powers systems like TLS / HTTPS and digital signatures, enabling secure data exchange without shared secret keys.
Hash functions ensure data integrity and are used heavily in authentication systems and verifying downloaded files.
Encoding is not encryption—it’s reversible and not intended for privacy/security.

