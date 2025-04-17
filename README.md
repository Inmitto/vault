# Inmitto Vault

## Prerequisites

- [password-store](https://www.passwordstore.org/#download)
- [GnuPG](https://gnupg.org/download/index.html)

## Setup

```bash
git clone git@github.com:Inmitto/vault.git ~/.password-store/inmitto 
cd ~/.password-store/inmitto

for key in pubkeys/*; do gpg --import $key; done;
for id in $(cat .gpg-id); do gpg --lsign $id; done;
```

Generate key if you do not already have one:
```bash
gpg --full-generate-key
gpg --armor --export [MAIL] > pubkeys/yourname.asc
git add .
git commit -m "Add [NAME] to public keys"
git push
```

## After New Member Joins

After a new member joins, each member that has already setup the vault must re-initialize and re-encrypt the data:
```bash
cd ~/.password-store/inmitto
git pull
gpg --import pubkeys/newuser.asc
gpg --lsign [MAIL OF NEW USER]
pass init -p inmitto $(cat .gpg-id)
git push
```

## Generate New Password

```bash
tr -dc 'A-Za-z0-9!#$%&/()=' </dev/urandom | head -c 24
```
