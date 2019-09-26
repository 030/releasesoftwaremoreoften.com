# git

## private key

[GitHub provides clear instructions](https://help.github.com/en/enterprise/\
2.16/user/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
how to create a private key and how to use it to perform git actions like
cloning repositories and pushing changes.

The bare minimum is creating a private key and adding the public key to a git
repository:

```
ssh-keygen -t rsa -b 4096 -C "some-user@some-domain"
```

Once this command is run, a password has to be entered. Finally, the public
key has to be copied and pasted to the git repository. One could issue:

```
cat ~/.ssh/id_rsa.pub
```

to get the content of the public key. Note: never check the content of the
private key as this is private and should remain on your laptop. If you
decided to clone repositories on a new laptop, never copy an existing
key, but create a new one! Ensure that you are the only person that is
allowed to read the private key, by running:

```
chmod 0400 ~/.ssh/id_rsa
```
