# Nginx Configuration - CENTOS 7
These configuration settings are strictly for NGINX on CENTOS


## INSTALLATION

```env
sudo yum install epel-release
sudo yum upgrade
```

### CONFIGURATION
Once Oracle Apex is running on ORDS you should be able to proceed to the next step, to verify if oracle apex is running on your server
```env
curl <IPADDRESS:8080>
```
OR visit your browser and check manually.

```env
sudo nano /etc/nginx/conf.d/yourdomain.conf
```
```env
server {
    server_name yourdomain;  # Replace with your domain name

    location / {
        proxy_pass http://localhost:8080/;
        proxy_set_header Origin "" ;
        proxy_set_header X-Forwarded-Host $host:$server_port;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_connect_timeout       600;
        proxy_send_timeout          600;
        proxy_read_timeout          600;
        send_timeout                600;
    }
}
```
To validate settings:
```env
sudo nginx -t
```
### Install Certbot
```env
sudo yum install certbot-nginx
```

#### Run Certbot to obtain SSL
```env
sudo certbot --nginx
```

## ERRORS TO LOOKOUT FOR

The Famous 502 Bad Gateway error. If you experience this it is more than likely SELINUX is either disable or Nginx doesn't have necessary permissions to proxy the requests.

Verify if selinux status
```env
sestatus
```

Verify the audit logs for nginx
```env
sudo grep nginx /var/log/audit/audit.log
```
Set SeEnforce
```env
sudo setenforce 0
```

Finally... restart nginx
```env
sudo systemctl restart nginx
```
