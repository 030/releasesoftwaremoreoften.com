# Release Software More Often

## 2021-03-30

Last year, a collegae of mine was playing a Tech video twice as fast during KubeCon. Today
I ordered a couple of order tech videos on Udemy. This website is also capable of playing
videos faster, which is really helpful as I can watch more Tech videos on a day and learn faster.
In order to speed up a video, navigate to the `settings`, click on `playback speed` and change it
to `1.5` or `2`.

## 2021-03-26 DIP (2.1.4)

In order to get the latest version of a docker image from dockerhub, one could use the [Docker Image Patrol (DIP) tool](https://github.com/030/dip). Either download the binary from the releases page, install if using [chocolatey](https://chocolatey.org/packages/dip) or install it using [snap](https://snapcraft.io/kdiutd). In order to get the latest version of golang:

```bash
kdiutd.dip -image=golang \
           -latest="^1\..*-alpine[0-9]+\.[0-9]+$" \
           -official
```

results in:

```bash
1.16.2-alpine3.13
```

## 2021-03-23 N3DR (6.0.6)

[Version 6.0.6 of N3DR](https://github.com/030/n3dr/compare/6.0.5...6.0.6) has been released. This version contains a `--skip-errors` option that allows users to continue-on-error while uploading Maven2 artifacts to Nexus3. Also two environment variables have been added to ensure that users could modify the regular expression to ensure that artifacts that deviate from the standard could be uploaded as well.

## 2020-05-09 BCBSN

I created the Bitbucket Cloud Build Status Notifier ([BCBSN](https://github.com/030/bcbsn)) to ensure that a build status can be sent to Bitbucket Cloud if a Jenkins Multi branch pipeline is run for the first time. [Initially I found a bug ticket, left a comment](https://issues.jenkins-ci.org/browse/JENKINS-40456) and tried to find a workaround, but after spending more than 10 hours it turned out that it was quicker to create a simple tool.

## 2020-05-04: N3DR

Over a year ago, I created a tool called Nexus3 Disaster Recovery ([N3DR](https://n3dr.releasesoftwaremoreoften.com/)). The reason was that I had to migrate the on-premise
Nexus to the cloud. Surprisingly there was not any tool available that was able to backup the artifacts from all repositories. I found a couple of different tools, but none of them was able to backup an entire Nexus. At the time of writing, the tool has 21 stars, two other people added some commits and a couple of questions were asked. Although it is not a very popular tool, it helped me and my colleagues to complete the migration to the cloud and we have no stress anymore whether we will loose Nexus data as an automatic backup is created everyday and the migration has proven that the disaster-recovery works as well.

## Why I prefer Ansible over other Configuration Management tools

I started to work with Ansible in 2017. The main reason was that nobody in the team mastered Puppet and there was one developer that liked Ansible. After using Puppet since 2012 and knowing the complete Domain Specific Language (DSL), creating own modules and publising them to Puppet Forge, implementing MCollective to enable push deployments it took far less time to get up to speed with Ansible as this Configuration Management (CM) tool has no DSL and the definitions have to be written in YAML. Another advantage is that installing Ansible on one system is sufficient and it leverages SSH instead of installing Puppet on the master, all slaves and using the Puppet certs.

|                      | ansible | chef | puppet | salt   |
|----------------------|---------|------|--------|--------|
| programming language | python  | ruby | ruby   | python |

Table 1: Differences between CM tools 

## If it hurts, do it more often

Back in the day, when a former colleague and I were talking about the three-monthly release,
he referred to an article of [Martin Fowler](https://martinfowler.com/bliki/FrequencyReducesDifficulty.html)
and added: "the reason that this four-times-a-year-release is so painful, is the time we did not release.
After three months, nobody knows how to release and shortcuts that were taken last time, will be taken again
due to deadline pressures". I totally agree with him and Martin Fowler. The article of the latter demonstrates
the exponential increase of pain, the longer a release gets postponed. Imagine the pain if a release would be
done once a year or two years...

## SOPS

[Secrets OPerationS](https://github.com/mozilla/sops) is a tool that is able
to manage secrets by using a Key Management Store like AWS KMS. The GitHub
README provides instructions how to get started with SOPS.

### September 26, 2019

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

## jenkins

### JCAC - Friday 20 September 2019

Today I was able to configure credentials and jobs using Jenkins Configuration As Code (JCAC).
[JCAC](https://github.com/jenkinsci/configuration-as-code-plugin) is a plugin that is able to
configure Jenkins without requiring manual changes in the UI. Initially I had to read something
more about how to get started. It turned out that just installing the configuration-as-code
plugin using ansible-geerlingguy-jenkins was insufficient as Jenkins did not want to start.
The logging indicated that multiple plugins were required.

In order to solve this, jenkins was booted, the JCAC was installed manually and once Jenkins
was restarted, it become obvious which dependent plugins are required. Once these plugins were
defined in Ansible, the Jenkins booted and the jenkins.yaml that has to be deployed in the
`/var/lib/jenkins` or `$JENKINS_HOME` was read. Unfortunately it turned out that the `plugins`
section support was dropped in the JCAC. Another impediment was the omission of certain plugins
when configuring jobs and credentials using JCAC. Fortunately, the jenkins log indicated which
plugins were omitted.

At the moment I have
[two challenges](https://gitter.im/jenkinsci/configuration-as-code-plugin?at=5d87457c5ab9361694381b5d):

1. [git-lfs](https://devops.stackexchange.com/q/9225/210)
1. [shallow-clone](https://devops.stackexchange.com/q/9229/210)

When creating an issue on Github JCAC, the documentation indicated that support questions should be
asked on [Gitter](https://gitter.im/jenkinsci/configuration-as-code-plugin).

Apart from these two issues, I like JCAC as it prevents that people have to configure a
Jenkins-master manually and that it becomes clear what changes were applied, instead of applying
archeology to find out what plugins were installed and why Jenkins is broken.

## git

### private key

[GitHub provides clear instructions](https://help.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
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
