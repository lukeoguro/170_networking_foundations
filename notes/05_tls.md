# TLS

## What to focus on

* Understand that TLS provides for secure message exchange over an unsecure channel
* Learn that there are multiple aspects of security

## TLS Protocol

* TLS stands for Transport Layer Security, and it started from SSL (Secure Socket Layer)
* Three important services:
  * Encryption — a process of encoding a message that can only be read with an authorized means of decoding the message
  * Authentication — a process to verify the identity of a particular party in the message exchange
  * Integrity — a process to detect whether a message has been interfered with or faked

## Encryption

* Cryptography is the use of techniques for securing communication
* A shared key system is known as a symmetric key encryption
  * In order for this to work security, the system relies on the sender and receiver both having the same keys
  * The question is, how do the sender and receiver exchange encryption keys in the first place?
* Asymmetric key encryption uses a pair of keys: a public key and a private key
  * The public key is used to encrypt and the private key to decrypt
  * Messages encrypted with the public key can only be decrypted with the private key
  * The public key is made openly available but the private key is kept in hte sole possession of the message receiver
* TLS Handshake
  * Uses a combination of symmetric and asymmetric cryptography
  * Initial symmetric key exchange is conducted using asymmetric key encryption
  * TLS handshake occurs after TCP handshake
  * Purpose is:
    * Agree which version of TLS is used
    * Agree on algorithms that will be included in cipher suite
    * Enable the exchange of symmetric keys
  * Steps:
    * Begins with `ClientHello` message sent from client to server after TCP `ACK`, and includes maximum version of TLS protocol and list of Cipher Suites
    * Server responds with `ServerHello`, and include certificate with public key and `ServerHelloDone`
    * Key exchange process
      * Client generates 'pre-master secret' and encrypts it with the server's public key, then sends in `ClientKeyExchange` along with `Finished` and `ChangeCipherSpec` flag
      * Server receives 'pre-master secret' and decrypts with private key
      * Both client and server uses the 'pre-master secret' to generate symmetric key
    * Server sends `ChangeCipherSpec` and `Finished`
* A cipher is a cryptographic algorithm — a cipher suite is a set of ciphers

## Authentication

* Certificate sent in `ClientHello` serves as a means of identification for the providing party (server)
* Includes various pieces of information, like who the owner is
* Server will include a signature encrypted with the private key in the certificate
* Certificate is also sent with original data, and upon receipt, client decrypts with public key and checks that data matches
* Issue is that a third-party can create their own key pair and also certificate identifying them
* Certificate Authorities (CAs) are a trustworthy source that issues certificates
* They validate the party requesting the certificate, and also digitally signs the certificate being issued with their own 'signature'
* There are 'Intermediate CA' and 'Root CA' along the chain of trust — Root CAs authenticate themselves and are the end-point
* This isn't fool-proof, but these Root CAs have gained reputation through prominence and longevity
* There are many Intermediate CAs, but few Root CAs

## Integrity

* TLS is the Session layer protocol in the OSI model
* Operates between HTTP and TCP
* TLS encapsulates data like any other PDUs in a record
* There is the MAC (Message Authentication Code) used like a checksum
* Yet, the difference is the implementation and intention
* Checksums were used for error detection — MAC is used to add a layer of security to verify data hasn't been altered or tampered
* Uses a hashing algorithm
  * Sender creates a digest of data payload with specific hashing algorithm with pre-agreed hash value
  * Receiver also creates a digest using the same algorithm and hash value, and makes sure the digests match
