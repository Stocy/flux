Originaly created using Funky Penguin's Geek Cookbook flux example

# Sops

Sops is used for encrypting some keys/fields in some yaml files to protect some confidential data.

## Explaination

The file `.sops.yaml` is used to indicate which file and which fields is protected
A single gpg private key is used for decrypting, the flux controller needs to be told which secret to get
As of now the secret `sops-gpg` in the `flux-system` namespace is used 

## General use 

**Important** : when a protected file is created, it can **not** be edited to add new protected fields, it needs to be re-created.

### Create a new protected file

**Mandatory** : ensure files and fileds concerned are indicated in `.sops.yaml`

* Directly : `sops encrypt -i <file>` ( test first without `-i` )
* Using an existing already encrypted file (Recreate) `file=<file> && sops decrypt $file | sops encrypt /dev/stdin --filename-override $file -i`

### Modify a protected file 

* `sops modify <file>`
