# SOPS

[Secrets OPerationS](https://github.com/mozilla/sops) is a tool that is able
to manage secrets by using a Key Management Store like AWS KWS. The GitHub
README provides instructions how to get started with SOPS.

## September 26, 2019

I created two keys in KMS, exported them by issuing:

```
export SOPS_KMS_ARN="arn1,arn2"
```

and subsequently I followed the README instructions and created my first
encrypted file using SOPS:

```
sops some-file.yml
```

When one opens this file, an encrypted content will be returned.
