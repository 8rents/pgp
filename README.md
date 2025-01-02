# PGP Keys

## Creating a new key pair

Using `gnupg` for all of our PGP needs.

```
gpg --full-generate-key
```

You  will be guided through the creation setting your name, choosing encryption type and bit length. I usually choose RSA with a 4096 bits.

## Export public key

```
gpg --output 8rents@gmail.com-public.pgp --armor --export 8rents@gmail.com
```

## Export private key

```
gpg --output 8rents@gmail.com-private.pgp --armor --export-secret-key 8rents@gmail.com 
```

## Encrypt Private key for upload

If you want to backup/store your private key in a public git repo you qill need to encrypt it with a password so that nobody else will be able to uae it.

```
gpg -a --symmetric --cipher-algo AES256 8rents@gmail.com-private.pgp
```

You will be asked to create a password which you will uze to decrypt the .asc file. Generate and save a strong password with a password manager. When complete you an encrypted .asc file will be created (`8rents@gmail.com-private.pgp.asc`).

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
