# Reveal password encrypted by SecureCRT

## 1. How does it work?

[how does SecureCRT encrypt password](HOW_DOES_IT_WORK.md)

## 2. How to use?

Please make sure you have installed python3 and module `pycryptodome`.

You can install the module by

```console
$ pip3 install pycryptodome
```

Usage:

```
$ ./SecureCRTCipher.py
Usage:
    SecureCRTCipher.py <enc|dec> [-v2] [-p ConfigPassphrase] <plaintext|ciphertext>

    <enc|dec>              "enc" for encryption, "dec" for decryption.
                           This parameter must be specified.

    [-v2]                  Encrypt/Decrypt with "Password V2" algorithm.
                           This parameter is optional.

    [-p ConfigPassphrase]  The config passphrase that SecureCRT uses.
                           This parameter is optional.

    <plaintext|ciphertext> Plaintext string or ciphertext string.
                           NOTICE: Ciphertext string must be a hex string.
                           This parameter must be specified.
```

## 3. Example

If you have SecureCRT session file `example.com.ini` looking like

```
S:"Username"=root
S:"Password"=
S:"Password V2"=02:7b9f594a1f39bb36bbaa0d9688ee38b3d233c67b338e20e2113f2ba4d328b6fc8c804e3c02324b1eaad57a5b96ac1fc5cc1ae0ee2930e6af2e5e644a28ebe3fc
S:"Login Script V2"=
...
...
```

You can reveal password by

```console
$ ./SecureCRTCipher.py dec -v2 7b9f594a1f39bb36bbaa0d9688ee38b3d233c67b338e20e2113f2ba4d328b6fc8c804e3c02324b1eaad57a5b96ac1fc5cc1ae0ee2930e6af2e5e644a28ebe3fc
DoubleLabyrinth
```
If the session file is generated by SecureCRT whose version is prior to 7.3.3, the sensitive data should be 

```
...
...
S:"Username"=root
D:"[SSH2] Port"=00000016
S:"Password"=uc71bd1c86f3b804e42432f53247c50d9287f410c7e59166969acab69daa6eaadbe15c0c54c0e076e945a6d82f9e13df2
D:"Session Password Saved"=00000001
...
...
```

You can reveal password by

```console
$ ./SecureCRTCipher.py dec c71bd1c86f3b804e42432f53247c50d9287f410c7e59166969acab69daa6eaadbe15c0c54c0e076e945a6d82f9e13df2
DoubleLabyrinth
```

