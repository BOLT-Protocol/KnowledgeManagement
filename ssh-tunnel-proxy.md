# ssh tunnel proxy

> source: [ngrok 不求人：自己搭一個窮人版的 ngrok 服務](https://5xruby.tw/posts/easy-ngrok-by-nginx-ssh-tunnel)

## step 1

要當 proxy 的主機安裝 nginx

`vim /etc/nginx/conf.d/default.conf`

```
server{
    listen 80;
    server_name explorer.cafeca.io;


    location ~* \.io {
        proxy_pass http://127.0.0.1:4000;

        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;
        proxy_redirect off;
    }

    location / {
        proxy_pass http://127.0.0.1:4000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
    }
}
```

## step 2

在本地 server 通過 ssh 指令建立連線，將本地 4000 port 映射到遠端 proxy，且為了使 ssh 連線一直保持著，所以這邊寫成了 daemon

`vim /etc/systemd/system/sshtunnel.service`

```
[Unit]
Description=SSH Tunnel
After=network.target

[Service]
Restart=always
RestartSec=20
User=blockchain
ExecStart=/usr/bin/ssh -NT -o ServerAliveInterval=60 -R 4000:localhost:4000 ubuntu@xxx.xxx.xxx.xxx -i xxx.pem

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl daemon-reload
sudo service sshtunnel start
sudo service sshtunnel status
sudo systemctl enable sshtunnel
```
