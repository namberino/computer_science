# Cryptography
Cryptography is a technique to secure data and communication. It is a method of protecting information and communications through the use of codes, so that only those for whom the information is intended can read and process it. Cryptography is used to protect data in transit, at rest, and in use. The prefix _crypt_ means "hidden" or "secret", and the suffix _graphy_ means "writing".

Cryptography prior to the modern age was effectively synonymous with encryption, converting readable information (plaintext) to unintelligible nonsense text (ciphertext), which can only be read by reversing the process (decryption). The sender of an encrypted (coded) message shares the decryption (decoding) technique only with intended recipients to preclude access from adversaries. The cryptography literature often uses the names "Alice" (or "A") for the sender, "Bob" (or "B") for the intended recipient, and "Eve" (or "E") for the eavesdropping adversary.[7] Since the development of rotor cipher machines in World War I and the advent of computers in World War II, cryptography methods have become increasingly complex and their applications more varied.

In Cryptography the techniques which are use to protect information are obtained from mathematical concepts and a set of rule based calculations known as algorithms to convert messages in ways that make it hard to decode it. These algorithms are used for cryptographic key generation, digital signing, verification to protect data privacy, web browsing on internet and to protect confidential transactions such as credit card and debit card transactions.

## Techniques used For Cryptography
In today’s age of computers cryptography is often associated with the process where an ordinary plain text is converted to cipher text which is the text made such that intended receiver of the text can only decode it and hence this process is known as encryption. The process of conversion of cipher text to plain text this is known as decryption.

## Encryption
Encryption is the process of converting plain text to cipher text. The process of encryption is done by using a key which is a secret code. The key is used to encrypt the plain text and the cipher text is obtained. The key is used to decrypt the cipher text and the plain text is obtained. The key is kept secret and is known only to the sender and the receiver of the message.

## Decryption
Decryption is the process of converting cipher text to plain text. The process of decryption is done by using a key which is a secret code. The key is used to decrypt the cipher text and the plain text is obtained. The key is used to encrypt the plain text and the cipher text is obtained. The key is kept secret and is known only to the sender and the receiver of the message.

## Types of Cryptography
There are two types of cryptography:
1. [Symmetric Cryptography](#symmetric-cryptography)
2. [Asymmetric Cryptography](#asymmetric-cryptography)

## Symmetric Cryptography
In symmetric cryptography the same key is used for encryption and decryption. The key is kept secret and is known only to the sender and the receiver of the message. The key is used to encrypt the plain text and the cipher text is obtained. The key is used to decrypt the cipher text and the plain text is obtained. The key is kept secret and is known only to the sender and the receiver of the message.

## Asymmetric Cryptography
In asymmetric cryptography two different keys are used for encryption and decryption. One key is used for encryption and the other key is used for decryption. The key used for encryption is known as public key and the key used for decryption is known as private key. The public key is made public and is known to everyone. The private key is kept secret and is known only to the sender and the receiver of the message. The public key is used to encrypt the plain text and the cipher text is obtained. The private key is used to decrypt the cipher text and the plain text is obtained. The key is kept secret and is known only to the sender and the receiver of the message.

## Hash Functions
Hash functions are used to map data of arbitrary size to data of fixed size. The values returned by a hash function are called hash values, hash codes, digests, or simply hashes. The values are used to index a fixed-size table called a hash table. Use of a hash function to index a hash table is called hashing or scatter storage addressing.

## Popular Cryptography Algorithms
1. [Caesar Cipher](notadded)
2. [Vigenere Cipher](notadded)
3. [Playfair Cipher](notadded)
4. [DES](notadded)
5. [AES](notadded)
6. [RSA](#rsa-rivest-shamir-adleman)
7. [Diffie-Hellman Key Exchange](notadded)
8. [ElGamal](notadded)
9. [Digital Signature Algorithm](notadded)
10. [Elliptic Curve Cryptography](notadded)

## RSA (Rivest-Shamir-Adleman)
**IMPORTANT NOTE**: 
    1. Do not implement techniques like these yourself in an environment, that can hurt you in any kind of way.
    2. The shown RSA method is already broken! This guide aims to give you a basic understanding of the algorithm.
Broken down, the RSA method is nothing more than the multiplicative inverse within a residue class ring.
This means that the task is to find an inverse modulo the Eulerian phi function of a high integer n that is difficult to compute.
This proves to be particularly difficult to do, as even computers have difficulties with the calculation algorithm above a certain length.
### Step 1: Finding n
To avoid this when generating the key, the n is chosen so that it is the product of two high prime numbers. This has the advantage that simple mathematical rules can be applied to determine the Phi of the product n.
The property that prime numbers and the Phi function share is that they are divisors of all numbers (except 1, but this does not play a role in the Phi function either) and therefore Phi of a prime number p is equal to p-1.
If you now want to determine the Phi of the product, you can simply multiply the prime numbers p and q as follows: $\Phi(n)=\Phi(p)\times\Phi(q)=(p-1)\times(q-1)$.
With this step, we have now determined our n and the phi of n.

### Step 2: Finding e
The next step is to search for our encryption exponent e. This is used to encrypt the message we are transmitting.
The n from step 1 and the e combined are therefore the public key with which messages can be encrypted.
The following steps must be observed when choosing a suitable e: 

1. **It must be co-prime to $\Phi(n)$**: The value of $e$ must have no common factors with $\Phi(n)$ except 1, which is expressed mathematically as $GCD(e, \Phi(n)) = 1$. This requirement ensures that $e$ has a unique multiplicative inverse modulo $\Phi(n)$. In simpler terms, there must be a number $d$ (which will be the decryption exponent) such that $e \times d$ is congruent to 1 modulo $\Phi(n)$.

2. **It must be within the range $1 < e < \Phi(n)$**: This range ensures that $e$ is a valid exponent for the modulo operation and helps maintain the encryption's mathematical properties.

    
This means that the e must be located in the residue class ring and is not a divisor of $\Phi(n)$.
A frequently used e is 65537, which is $2^{16}+1$ and a prime number.

Now we have our public key composed of n and e and can encrypt messages m as follows: $c=m^{e}\ mod\ n$

### Step 3: Private Key
As mentioned above, the private key consists of the multiplicative inverse of our encryption exponent in the remainder class ring $\Phi(n)$.
So there is nothing more to do than to calculate $d=e^{-1}\ mod\ \Phi(n)$.
We have to do this using the extended Euclidean algorithm, for which there are various approaches.

To decrypt a received ciphertext, we have to exponentiate it with our private key:

$m'=c^d\ mod\ n$

### Example
In the following I will give a small example of the RSA calculation. This is carried out with comparatively tiny integers and is purely for demonstration purposes.
We are given the prime numbers $p=23$ and $q=31$. Our n is therefore 

$n=p\times q=23\times 31=713$.

#### Step 1: $\Phi(n)$
As shown above, we do a simple calculation:

$\Phi(n)=\Phi(p)\times \Phi(q)=(p-1)\times (q-1)=30\times 22=660$

#### Step 2: Encryption exponent e
I have chosen a small value for demonstration purposes.
Let $e=7$
We can now show that the above rules are observed:
1. $1<7<660$
2. $GCD(7,660)=1$

#### Step 3: Decryption exponent d
As already mentioned above, there are various techniques for applying the extended Euclidean algorithm. 
In the example, a table form is used in which the following formulae apply:
1. $a_{i+1}=b_i$
2. $b_{i+1}=r_i$
3. $x_i=y_{i+1}$
4. $y_i=x_{i+1}-q_i\times x_i$
5. $x_n=0$ ^ $y_n=1$

We remember that the decryption exponent is calculated as follows: $d=e^{-1}\ mod\ \Phi(n)$

We determine this as follows: 

| i | a   | b | q  | r | x  | y   |
|---|-----|---|----|---|----|-----|
| 1 | 660 | 7 | 94 | 2 | -3 | 283 |
| 2 | 7   | 2 | 3  | 1 | 1  | -3  |
| 3 | 2   | 1 | 2  | 0 | 0  | 1   |

The procedure is quite simple. We calculate our $\Phi(n)$ modulo our e and work our way down from there until we have a remainder of 0. Until then, x and y remain empty.
When we have the remainder 0, we insert the standard values for x and y and work our way up again from below

__NOTE__: 
```
1. *RSA* means Rivest–Shamir–Adleman. 
2. *DES* means Data Encryption Standard. 
3. *AES* means Advanced Encryption Standard.
```

## Features Of Cryptography are as follows:

### Confidentiality:
Information can only be accessed by the person for whom it is intended and no other person except him can access it.
### Integrity:
Information cannot be modified in storage or transition between sender and intended receiver without any addition to information being detected.
### Non-repudiation:
The creator/sender of information cannot deny his intention to send information at later stage.
### Authentication:
The identities of sender and receiver are confirmed. As well as destination/origin of information is confirmed.


## [Crypto Currency](CryptoCurrency/readme.md)
Crypto currency is a digital currency in which encryption techniques are used to regulate the generation of units of currency and verify the transfer of funds, operating independently of a central bank. Cryptocurrencies use decentralized control as opposed to centralized digital currency and central banking systems. The decentralized control of each cryptocurrency works through distributed ledger technology, typically a blockchain, that serves as a public financial transaction database. A defining feature of a cryptocurrency, and arguably its most endearing allure, is its organic nature; it is not issued by any central authority, rendering it theoretically immune to government interference or manipulation.

## Features of Crypto Currency are as follows:
1. Decentralized
2. Anonymous
3. Secure
4. Transparent
5. Immutable
6. Fast

## Types of Crypto Currency are as follows:
1. [Proof of Work](#proof-of-work)
2. [Proof of Stake](#proof-of-stake)

### [Proof of Work](CryptoCurrency/ProofOfWork/readme.md)
Proof of work (PoW) describes a system that requires a not-insignificant but feasible amount of effort in order to deter frivolous or malicious uses of computing power, such as sending spam emails or launching denial of service attacks. The concept was subsequently adapted to securing digital money by Hal Finney in 2004 through the idea of "reusable proof of work" using the SHA-256 hashing algorithm.

### _Most Popular Proof of Work Crypto Currency are as follows:_
1. [Bitcoin](CryptoCurrency/ProofOfWork/Bitcoin/readme.md)
2. [Litecoin](CryptoCurrency/ProofOfWork/Litecoin/readme.md)
3. [Dogecoin](CryptoCurrency/ProofOfWork/Dogecoin/readme.md)

### [Proof of Stake](CryptoCurrency/ProofOfStake/readme.md)
Proof-of-stake is a cryptocurrency consensus mechanism for processing transactions and creating new blocks in a blockchain. A consensus mechanism is a method for validating entries into a distributed database and keeping the database secure. In the case of cryptocurrency, the database is called a blockchain—so the consensus mechanism secures the blockchain.

### _Most Popular Proof of Stake Crypto Currency are as follows:_
1. [Ethereum](CryptoCurrency/ProofOfStake/Ethereum/readme.md)
2. [EOS](CryptoCurrency/ProofOfStake/EOS/readme.md)
3. [Cardano](CryptoCurrency/ProofOfStake/Cardano/readme.md)


## [Blockchain](Blockchain/readme.md)
Blockchain is a distributed database that maintains a continuously growing list of ordered records called blocks. Each block contains a cryptographic hash of the previous block, a timestamp, and transaction data. By design, a blockchain is resistant to modification of the data. It is "an open, distributed ledger that can record transactions between two parties efficiently and in a verifiable and permanent way".

## Features of Blockchain are as follows:
1. Decentralized
2. Immutable
3. Transparent
4. Secure

## Types of Blockchain are as follows:
1. [Public Blockchain](#public-blockchain)
2. [Private Blockchain](#private-blockchain)
3. [Permissioned Blockchain](#permissioned-blockchain)

### [Public Blockchain](Blockchain/PublicBlockchain/readme.md)
A public blockchain is a blockchain that is accessible to anyone. Public blockchains are open to anyone who wants to participate in the network. This means that anyone can view the blockchain and its transactions, and anyone can participate in the network by mining and validating transactions. Public blockchains are also known as permissionless blockchains.

## Advantages
A public network operates on an incentivizing scheme that encourages new participants to join and keep the network agile. Public blockchains offer a particularly valuable solution from the point of view of a truly decentralized, democratized, and authority-free operation.


Public blockchains are extraordinarily valuable because they can serve as a backbone for nearly any decentralized solution. Additionally, the vast number of network participants joining a secured public blockchain keeps it safe from data breaches, hacking attempts, or other cybersecurity issues. The more participants, the safer a blockchain is.

Public blockchains can be secured with automatic validation methods and encryption that keep single entities from changing information in the chain (like cryptocurrency blockchains), or they can allow anyone to make changes..

## Disadvantages
The primary disadvantage to secured public blockchains is the heavy energy consumption required to maintain them. The concern is a consensus mechanism that requires participants to compete to validate the information and receive a reward for letting the network use their processing power. Not all blockchain networks use an energy-intensive validation process, so not all use enormous amounts of electricity.

Other issues include the lack of complete privacy and anonymity. Public blockchains allow anyone to view transaction amounts and the addresses involved. If the address owners become known, the user loses their anonymity.

Public blockchains also attract participants who may not be honest in their intentions. Most public blockchains are designed for cryptocurrencies, which by nature of their value are a prime target for hackers and thieves which is very useful.

### [Private Blockchain](Blockchain/PrivateBlockchain/readme.md)
A private blockchain is a blockchain that is only accessible to a select group of people. Private blockchains are not open to the public. This means that only a select group of people can view the blockchain and its transactions, and only a select group of people can participate in the network by mining and validating transactions. Private blockchains are also known as permissioned blockchains.
Private blockchains control who is allowed to participate in the network. If the network is capable of mining, its private nature could control which users can execute the consensus protocol that decides the mining rights and rewards. Additionally, only select users might maintain the shared ledger. The owner or operator has the right to override, edit, or delete the necessary entries on the blockchain as required or as they see fit.

## Advantages
A private blockchain is not decentralized. It is a distributed ledger that operates as a closed database secured with cryptographic concepts and the organization's needs. Only those with permission can run a full node, make transactions, or validate/authenticate the blockchain changes.

By reducing the focus on protecting user identities and promoting transparency, private blockchains prioritize efficiency and immutability—the state of not being able to be changed.

These are important features in supply, logistics, payroll, finances, accounting, and many other enterprise and business areas.

## Disadvantages
While purposefully designed for enterprise applications, private blockchains lose out on many of the valuable attributes of permissionless systems simply because they are not widely applicable. They are instead built to accomplish specific tasks and functions.

In this respect, private blockchains are susceptible to data breaches and other security threats. This is because there is generally a limited number of validators used to reach a consensus about transactions and data if there is a consensus mechanism.

In a private blockchain, there may not be consensus but only the immutability of entered data unless an operator or administrator can make changes.

## [Permissioned Blockchain](Blockchain/PermissionedBlockchain/readme.md)
Permissioned blockchains are a mix between the public and private blockchains and support many options for customization.

## Advantages
Permissioned blockchain advantages include allowing anyone to join the permissioned network after a suitable identity verification process. Some give special and designated permissions to perform only specific activities on a network. This allows participants to perform particular functions such as reading, accessing, or entering information on the blockchain.

Permissioned blockchains allow for many functions, but one most interesting to businesses is Blockchain-as-a-Service (BaaS)—a blockchain designed to be scalable for the needs of many companies or tasks that the providers rent out to other businesses.

Blockchain-as-a-Service reduces costs for many businesses that can benefit from using blockchain technology in their business processes.

For example, say a business wants to improve transparency and accuracy in its accounting processes and financial reporting. It could rent blockchain accounting services from a BaaS provider. The blockchain would provide an interface where entries are made by end users and then automates the rest of the accounting processes.

In this way, there are fewer errors and no way for other parties to alter financial data after it is entered. As a result, financial reports to management and executives become more accurate, and the blockchain is accessible for viewing and generating real-time financial reports.

The business might choose to have its invoicing, payments, book-keeping, and tax reporting automated. Additionally, blockchain can prevent anyone with dishonest intentions from altering financial data or taking advantage of weaknesses in accounting processes.
Disadvantages
The disadvantages of permissioned blockchains mirror those of public and private blockchains, depending on how they are configured. One key disadvantage is that because permissioned blockchains require internet connections, they are vulnerable to hacking. By design, some might use immutability techniques such as cryptographic security measures and validation through consensus mechanisms.

While most blockchains are thought to be unhackable, there are weaknesses. Cryptocurrency theft occurs when a network is hacked into, and private keys are stolen. Permissioned blockchains also suffer this weakness because the networks that connect the users to the service depend on security measures that can be bypassed. User information can be stolen and accounts hacked into, similar to enterprise-level data breaches like the one Target suffered in 2013 when a third-party with access to the network was hacked.

