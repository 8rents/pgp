[Readme](../README.md) | [PGP Documentation Table of Contents](README.md)

---

# GnuPG 2.5.17 Help Dump

The following is a dump of the gnupg help page and formatted into markdown.

**Home folder**: `/data/data/com.termux/files/home/.gnupg`

## Supported algorithms

- **Pubkey**: `RSA`, `Kyber`, `ELG,` `DSA`, `ECDH`, `ECDSA`, `EDDSA`
- **Cipher**: `IDEA`, `3DES`, `CAST5`, `BLOWFISH`, `AES`, `AES192`, `AES256`, `TWOFISH`, `CAMELLIA192`, `CAMELLIA256`
- **Hash**: `SHA1`, `RIPEMD160`, `SHA256`, `SHA384`, `SHA512`, `SHA224`
- **Compression**: Uncompressed, `ZIP`, `ZLIB`, `BZIP2`

## Syntax

```
 gpg [options] [files]
```

Default operation depends on the input data. Sign, check, encrypt or decrypt.

---

## Commands

Here is the command help dump helpfully sorted by topic

### Working with the system Keyring

The system keyring holds all of a users public and private keys securely

---

### Making New Keys

- `--generate-key` - generate a new key pair
- `--quick-generate-key` - quickly generate a new key pair
- `--full-generate-key` - full featured key pair generation

---

### Preventing Mistakes

- `-n`, `--dry-run` - do not make any changes
- `-i`, `--interactive` - prompt before overwriting

### Input / Output Settings

- `-v, --verbose` - verbose
- `-q, --quiet` - be somewhat more quiet
- `--options FILE` - read options from FILE
- `--log-file FILE`- write server mode logs to FILE

---

###  Working with system Keyring


#### Keyrimg Configuration Options

- `--default-key <NAME>` - use NAME as default secret key
- `--group <SPEC>` - set up email aliases
- `--openpgp`- use strict OpenPGP behavior

#### Listing Keys

- `-k`, `--list-keys` - list keys
- `--list-signatures` - list keys and signatures
- `--fingerprint` - list keys and fingerprints
- `-K`, `--list-secret-keys` - list secret keys

#### Modifying Keys

- `--quick-add-uid` - quickly add a new user-id
- `--quick-revoke-uid` - quickly revoke a user-id
- `--quick-set-expire` - quickly set a new expiration date
- `--change-passphrase` - change a passphrase
- `--tofu-policy <VALUE>`  set the TOFU policy for a key

#### Deleting Keys

- `--generate-revocation` - generate a revocation certificate
- `--delete-keys` - remove keys from the public keyring
- `--delete-secret-keys` - remove keys from the secret keyring

#### Importing / Exporting from the Keyring

- `--export` - export keys
- `--import` - import/merge keys
- `--auto-key-locate MECHANISMS` - use MECHANISMS to locate keys by mail address
- `--auto-key-import` - import missing key from a signature
- `--include-key-block` - include the public key in signatures
- `--disable-dirmngr`  - disable all access to the dirmngr

---

### Encrypting / Decrypting Data

- `-e`, `--encrypt` - encrypt data
- `-c`, `--symmetric` - encryption only with symmetric cipher
- `-d`, `--decrypt` - decrypt data (default)

- `-r`, `--recipient USER-ID`  - encrypt for USER-ID
- `-u`, `--local-user USER-ID` - use USER-ID to sign or decryp/t
- `--encrypt-to <NAME>` - encrypt to user ID NAME as well

#### Encrypted data Output

 - `-a`,` --armor` - create ascii armored output
 - `-o`, `--output <FILE>` - write output to FILE
 - `-z <N>` - set compress level to N (0 disables)

---

### Signing Keys

- `-s`, `--sign` - make a signature
- `--clear-sign` - make a clear text signature
- `--quick-sign-key` - quickly sign a key
- `--quick-lsign-key` - quickly sign a key locally 
- `--quick-tsign-key` - quickly sign a key with a trust signature
- `--quick-revoke-sig` - quickly revoke a key signature
- `--sign-key` - sign a key
- `--lsign-keysign` - sign a key locally
- `--edit-key` - sign or edit a key
- `-b`, `--detach-sign` - make a detached signature
 - `--check-signatures` -  list and check key signatures
 - `--verify` - verify a signature

---

### Working with a Key Server

- `--search-keys` -  search for keys on a keyserver
- `--send-keys` -  export keys to a keyserver
- `--receive-keys` - import keys from a keyserver
- `--refresh-keys` - update all keys from a keyserver

#### Running a Keyserver

- `--server` - run in server mode

---

### Working with Cards

- `--card-status` - print the card status
- `--edit-card` - change data on a card
- `--change-pin` - change a card's PIN
- `--update-trustdb` - update the trust database
- `--print-md` - print message digests

> *See the man page for a complete listing of all commands and options*

---

## Examples

sign and encrypt for user Bob

```
-se -r Bob [file]   
```
 
make a clear text signature


```
--clear-sign [file]     
```

Make a detached signature


```
--detach-sign [file]       
```

show keys
 

```
--list-keys [names]      
```

show fingerprints

```
--fingerprint [names]    
```

---

Please report bugs to: <https://bugs.gnupg.org>