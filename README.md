```bash
sudo nvim /etc/nginx/sites-available/my-wordpress
```

```nginx
server {
    listen 80;
    server_name wordpress.google.com;

    client_max_body_size 128M;

    location / {
        proxy_pass http://127.0.0.1:8081;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}

```

```bash
sudo ln -s /etc/nginx/sites-available/my-wordpress /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx

```

