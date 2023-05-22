# Custom Application Nginx Configuration - CENTOS 7
These configuration settings are strictly for NGINX on CENTOS to redirect custom apps from a domain of your choice

### CONFIGURATION
```env
sudo nano /etc/nginx/conf.d/yourdomain.conf
```
```env
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:8080;
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

    location = / {
        rewrite ^/$ /ords/f?p=100 permanent;
    }

    if ($scheme = http) {
        return 301 https://$host$request_uri;
    }
}
```
To validate settings:
```env
sudo nginx -t
```
To restart nginx

```env
sudo systemctl nginx restart
```
