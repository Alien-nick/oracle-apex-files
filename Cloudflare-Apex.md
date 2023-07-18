### Cloudflare Firewall Configuration
To move over to cloudflare you will need to add reconfigure your nameservers.

![Cloudflare Name Server](https://castechblogdocs.s3.amazonaws.com/cloudflare-ns.png)

Then add your domain you will want to use, lets say example.com then you can point your records whether its (A, CNAME, TXT etc)

![Cloudflare DNS](https://castechblogdocs.s3.amazonaws.com/cloudflare-dns.png)

Ensure the DNS is proxied. This will ensure your server IP remains hidden.

Head over to security -> WAF, your dashboard should be looking like this

![WAF](https://castechblogdocs.s3.amazonaws.com/cloudflare-waf.png)

Hit create rule

![Rules](https://castechblogdocs.s3.amazonaws.com/cloudflare-waf-rules.png)

Then configure your rule set to match these criterias.

Once successfully configured, you will be able to see your event logs as:

![CloudflareLogs](https://castechblogdocs.s3.amazonaws.com/cloudflare-logs.png)

![Block](https://castechblogdocs.s3.amazonaws.com/cloudflare-block.png)
