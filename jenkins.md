# jenkins

## JCAC - Friday 20 September 2019

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
