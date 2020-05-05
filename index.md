# Release Software More Often

## Why I prefer Ansible over other Configuration Management tools

I started to work with Ansible in 2017. The main reason was that nobody in the team mastered Puppet and there was one developer that liked Ansible. After using Puppet since 2012 and knowing the complete Domain Specific Language (DSL), creating own modules and publising them to Puppet Forge, implementing MCollective to enable push deployments it took far less time to get up to speed with Ansible as this Configuration Management (CM) tool has no DSL and the definitions have to be written in YAML. Another advantage is that installing Ansible on one system is sufficient and it leverages SSH instead of installing Puppet on the master, all slaves and using the Puppet certs.

## If it hurts, do it more often

Back in the day, when a former colleague and I were talking about the three-monthly release,
he referred to an article of [Martin Fowler](https://martinfowler.com/bliki/FrequencyReducesDifficulty.html)
and added: "the reason that this four-times-a-year-release is so painful, is the time we did not release.
After three months, nobody knows how to release and shortcuts that were taken last time, will be taken again
due to deadline pressures". I totally agree with him and Martin Fowler. The article of the latter demonstrates
the exponential increase of pain, the longer a release gets postponed. Imagine the pain if a release would be
done once a year or two years...

## Preferred technologies

| Type                     | Technology           |
|:-------------------------|:---------------------|
| CI                       | [Jenkins](jenkins.md)|
| Configuration Management | [Ansible](ansible.md)|
| Container Orchestration  | Kubernetes           |
| Cloud                    | AWS                  |
| IDE                      | VS Code              |
| Infrastructure as Code   | Terraform            |
| Operating System         | Linux                |
| Programming              | Golang               |
| Scripting                | Bash                 |
| Secret Management        | [SOPS](sops.md)      |
| Serverless               | Lambda               |
| Software Repository      | Nexus3               |
| Text Editor              | Vim                  |
| VCS                      | [Git](git.md)        |
| VMs as Code              | Packer               |

## Tools

* <https://bcbsn.releasesoftwaremoreoften.com/>
* <https://dip.releasesoftwaremoreoften.com/>
* <https://go-multipart.releasesoftwaremoreoften.com/>
* <https://go-yq.releasesoftwaremoreoften.com/>
* <https://informado.releasesoftwaremoreoften.com/>
* <https://n3dr.releasesoftwaremoreoften.com/>
