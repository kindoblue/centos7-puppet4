# docker-centos7-puppet4
Docker image for puppet server v.4

Autosigning is turned *on* in puppet.conf.

To use this container:
---

1. `docker run -d -v /<<your-host-dir>>:/opt/puppetlabs/code --name puppetmaster -h puppet -p 8140:8140 kindoblue/docker-centos7-puppet4`
3. **Important**, to initialize the codedir of puppet master: `docker exec puppetmaster  cp -Rf /etc/puppetlabs/code/ /opt/puppetlabs/`
3. To see list of certs: `docker exec puppetmaster /opt/puppetlabs/bin/puppet cert list -all`
4. To test on a client:
	1. Install Puppet, Hiera, Facter, and Puppet LaunchDaemon onto client
	2. Add the IP of your Docker host to /etc/hosts (or configure DNS so that your Docker host is reachable at "puppet").  For example:  
		"10.0.0.1	puppet"
	3. Test puppet on client running as root:  
		`/opt/puppetlabs/bin/puppet agent --test`
		You should see the cert request being generated and autosigned.
5. To create manifestsi for the preexisting environment, place them in `/<<your-host-dir>/environments/production/manifests` 
