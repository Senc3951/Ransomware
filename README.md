# Ransomware
In this project I created a Ransomware using C#.

## How it works
First the program will check if it's running on a testing machine like: VM, sandbox...
If yes, it will destroy it self, else the process starts:

The system reboots into safe mode (if it's not already in it), because on safe mode most drives are disabled then no AV works (Shadow copies don't work on this mode).
Then the program gets elevated privileges using UAC bypass to perform certain registry changes and access certain files.

[The Ransomware will have the Server's RSA-512 PublicKey hardcoded]
Once it has admin privileges, the program generates a unique RSA-512 pair, and encrypt the PrivateKey using the ServerPublicKey.
Then it crawls through all the drives using MultiThreading, and each file is encrypted using a newly generated AES-256.

Each AES key is then encrypted using the ClientPublicKey, and with that, the encryption ends, the program drops a Message on the desktop and destroys it self.

In order to decrypt all the files, each AES key needs to be decrypted using the ClientPrivateKey, but as it is encrypted with the ServerPublicKey, the victim needs the ServerPrivateKey, and this is where the payment comes in.
