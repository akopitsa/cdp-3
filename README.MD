vim /etc/puppetlabs/puppet/r10k.yaml


commands
pull Puppetfile
/opt/puppetlabs/puppet/bin/r10k deploy environment production(branches) -v
/opt/puppetlabs/puppet/bin/r10k deploy environment production(branches) -pv


pull all branches

/opt/puppetlabs/puppet/bin/r10k deploy environment  -pv

