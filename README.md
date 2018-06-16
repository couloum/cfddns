# cfddns
Cloudflare Dynamic DNS 

Update one or several records from Cloudflare with the public IP of your server. This replaces any dynamic DNS service.

This project is based on benkulbertis work (https://gist.github.com/benkulbertis/fff10759c2391b6618dd).

I improved the original script with the following things:
- Separate configuration file to store Cloudflare credentials
- Possibility to update several records
- If update fail, try to update the record during the next launch
- Better management of errors during execution
- Use standard logging dir and var dir

# Installation

```shell
cp cfddns /usr/local/sbin/
cp cfddns.conf /etc/
# Change cfddns.conf with your own settings
chmod 640 /etc/cfddns.conf
cp cfddns.logrotate /etc/logrotate.d/cfddns
echo "*/5 * * * * root /usr/local/sbin/cfddns" > /etc/cron.d/cfddns
```

# Configuration

The configuration file looks like that:

```
# Your cloudflare account login
auth_email="name@domain.com"

# Your cloudflare token, found in your profile settings
auth_key="<32 characters key>"

# URL of a service that can provide you your public IP
# This URL must return only the public IP, with no other text
pub_ip_discovery_url="http://ipv4.icanhazip.com"

# Your zone to update
zone_name="domain.com"

# Space separated list of records to update (they all must belong to the same zone)
records="record1.domain.com record2.domain.com"
```

# Todo

List of things that still could be improved:
- Possibility to update more than one zone
- Possibility to override parameters from configuration file with arguments provided in command line
- Add verbosity
- Update records AAAA field if host has an IPv6
- Create record if not existant
