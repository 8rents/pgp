# PGP Keys

> *How to creatte a new master keypair from scratch for identity and then create a git commit signing sub key to sign all git commits with in vigilant mode*

---

## In this Docuement

- [Creating a new master key pair](#creating-a-new-master-key-pair)

---


## Creating a new master key pair

First make sure that `gnupg` is installed. Once you can confirm it is we will go ahead and create a new master key pair. 

```
gpg --full-generate-key
```

You  will be guided through the creation setting your name, choosing encryption type and bit length. I usually choose RSA with a 4096 bits.

### Wait... Whatdaya mean a "master key pair"?

PGP works a little bit different than other cryptographicc key systems (like SSH), With PGP The first keypair that you make will be the master key pair. The "master key" will be used to identify you. it will be the basis of your cryptographic identity.

#### Cryptograpyic Identity??!?

The basic gist of PGP is you have a master public / private key pair. Then you create sub keys off of these master keys. You can create sub-keys to encrypt data, authenticate and sign messages.

## Upload your public key to a key server

You can use the pgp `--send-keys` command, specifying the `key-ID` (the last 8 characters of my key fingerprint. The default keyserver is [keys.openpgp.org](https://keys.openpgp.org/).

## Import a Public key (to your keychain)

Your keychain can keep track of all the trusted keys you've used. To import a key to your keychain:

```
gpg --import <keyfile>
```

## Export public key 

You could export a public key to upload it to a key server, send it to a friend, or back it up on external media.

> __Options used in the following command:__
>
> `--output` - Path to the output file to be created
> `--armor` - Encrypt the output file in ASCII, not binary.
> `--export` - which public key you are exporting
> `--export-secret-key` - which private key to export

```
gpg --output 8rents@gmail.com-public.asc --armor --export 8rents@gmail.com
```

## Export private key

Exporting your private key is a much more sensitive operation.

```
gpg --output 8rents@gmail.com-private.asc --armor --export-secret-key 8rents@gmail.com 
```

## Encrypt Private key for upload to a private git repo

If you want to backup/store your private key in a public git repo you will need to encrypt it with a password so that nobody else will be able to uae it.


> __Options used in the following command:__
>
> `--symmetric` - Use a password to encrypt the data (not another key)
> `--cipher-algo` - which algorithm to use as a cipher (for encryption)

```
gpg -a --symmetric --cipher-algo AES256 8rents@gmail.com-private.pgp --armor
```

You will be asked to create a password which you will uze to decrypt the .asc file. Generate andcrear save a strong password with a password manager. When complete you an encrypted .asc file will be created (`8rents@gmail.com-private.pgp.asc`).

Make sure to create a `.gitignore` file with the unencrypted file name in it.

```
touch .gitignore && echo 8rents@gmail.com-private.pgp >> .gitignore 
```

This way only the encrypted private key (.asc file) will be committed and uploaded.

Confirm it ia being ignored by running `git status`.

## Decrypt Private key to import

When you want to use your encrypted private key again you will use gpg to decrypt it with the password you set.

```
gpg --decrypt 8rents@gmail.com-private.pgp.asc
```

When complete you will have the decrpyted file `8rents@gmail.com-private.pgp`.
