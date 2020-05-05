# Ansible

I started to work with Ansible in 2017. The main reason was that nobody in the team mastered Puppet and there
was one developer that liked Ansible. After using Puppet since 2012 and knowing the complete Domain Specific
Language (DSL), creating own modules and publising them to Puppet Forge, implementing MCollective to enable push
deployments it took far less time to get up to speed with Ansible as this Configuration Management (CM) tool has
no DSL and the definitions have to be written in YAML. Another advantage is that installing Ansible on one system
is sufficient and it leverages SSH instead of installing Puppet on the master, all slaves and using the Puppet certs.
