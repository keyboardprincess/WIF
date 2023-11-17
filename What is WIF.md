## What is WIF?
Abbreviation of Wallet Import Format (WIF, also known as Wallet Export Format) is a way of encoding a private ECDSA key so as to make it easier to copy.

A **private key**  is a secret code that allows bitcoins to be spent.

In order to make copying of private keys less prone to error, Wallet Import Format may be utilized. WIF uses [base58Check](https://bitcoin.org/en/glossary/base58check "The method used in Bitcoin for converting 160-bit hashes into P2PKH and P2SH addresses.  Also used in other parts of Bitcoin, such as encoding private keys for backup in WIP format.  Not the same as other base58 implementations.") encoding on a private key, greatly decreasing the chance of copying error, much like standard Bitcoin addresses.

1.  Take a private key.
    
2.  Add a 0x80 byte in front of it for mainnet addresses.
    
3.  Append a 0x01 byte after it if it should be used with [compressed public keys](https://bitcoin.org/en/glossary/compressed-public-key "An ECDSA public key that is 33 bytes long rather than the 65 bytes of an uncompressed public key."). Nothing is appended if it is used with uncompressed public keys.
    
4.  Perform a SHA-256 hash on the extended key.
    
5.  Perform a SHA-256 hash on result of SHA-256 hash.
    
6.  Take the first four bytes of the second SHA-256 hash; this is the checksum.
    
7.  Add the four checksum bytes from point 5 at the end of the extended key from point 2.
    
8.  Convert the result from a byte string into a [Base58](https://en.wikipedia.org/wiki/Base58 "The method used in Bitcoin for converting 160-bit hashes into P2PKH and P2SH addresses.  Also used in other parts of Bitcoin, such as encoding private keys for backup in WIP format.  Not the same as other base58 implementations.") string using [Base58Check](https://bitcoin.org/en/glossary/base58check "The method used in Bitcoin for converting 160-bit hashes into P2PKH and P2SH addresses.  Also used in other parts of Bitcoin, such as encoding private keys for backup in WIP format.  Not the same as other base58 implementations.")
    

The process is easily reversible, using the Base58 decoding function, and removing the padding.

When importing or sweeping ECDSA private keys, a shorter format known as [wallet import format](https://en.bitcoin.it/wiki/Wallet_import_format "Wallet import format") is often used, which offers a few advantages. The wallet import format is shorter, and includes built-in error checking codes so that typos can be automatically detected and/or corrected (which is impossible in hex format) and type bits indicating how it is intended to be used. Wallet import format is the most common way to represent private keys in Bitcoin. For private keys associated with uncompressed public keys, they are 51 characters and always start with the number 5 on mainnet (9 on testnet).  Private keys associated with compressed public keys are 52 characters and start with a capital L or K on mainnet (c on testnet). This is the same private key in (mainnet) wallet import format:

```
5Kb8kLf9zgWQnogidDA76MzPL6TsZZY36hWXMssSzNydYXYB9KF
```

When a WIF private key is imported, it always corresponds to exactly one [Bitcoin address](https://allprivatekeys.com/bitcoin-address-format.php "Address"). Any utility which performs the conversion can display the matching Bitcoin address. The mathematical conversion is somewhat complex and best left to a computer, but it's notable that the WIF guarantees it will always correspond to the same address no matter which program is used to convert it.

The Bitcoin address implemented using the sample above is:  [1CC3X2gu58d6wXUWMffpuzN9JAfTUWu4Kj](https://apirone.com/btc/address/1CC3X2gu58d6wXUWMffpuzN9JAfTUWu4Kj)
