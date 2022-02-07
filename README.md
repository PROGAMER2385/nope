# Reliactyl-Premium
Reliactyl Client Premium Version
<hr>
<h1>Features</h1>
- Allows users to split resources throughout multiple servers on the Pterodactyl Panel, and uses a Discord OAuth2 as a login system.<br>
- Coins (AFK Page earning, Linkvertise earning)<br>
- Coupons (Gives resources & coins to a user)<br>
- Servers (create, view, edit servers)<br>
- Store (buy resources with coins)<br>
- User System (auth, regen password, profile)<br>
- Join for Resources (join discord servers for resources)<br>
- API (for bots & other things)<br>

# Installination-Setup
<h2>Installing Dependencies</h2>

`sudo apt update && sudo apt upgrade`
`curl -fsSL https://deb.nodesource.com/setup_14.x | sudo bash -`
`apt install nodejs`
`npm -v`
`apt install nginx`
`sudo apt install certbot`
`sudo apt install -y python3-certbot-nginx`
```
<h2>Webserver Config</h2>

`systemctl start nginx`
`certbot certonly --nginx -d your.domain`
`nano /etc/nginx/sites-enabled/reliactyl.conf`
`# In reliactyl, paste this config and change the varible `
```Nginx
server {
    listen 80;
    server_name <domain>;
    return 301 https://$server_name$request_uri;
}
server {
    listen 443 ssl http2;
location /afkwspath {
  proxy_http_version 1.1;
  proxy_set_header Upgrade $http_upgrade;
  proxy_set_header Connection "upgrade";
  proxy_pass "http://localhost:<port>/afkwspath";
}
    
    server_name <domain>;
ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols SSLv3 TLSv1 TLSv1.1 TLSv1.2;
    ssl_ciphers  HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    access_log /var/log/nginx/access.log;
location / {
      proxy_pass http://localhost:<port>/;
      proxy_buffering off;
      proxy_set_header X-Real-IP $remote_addr;
  }
}
```
<h2>Starting Reliactyl</h2>

`1. Testing`
`cd path/to/the/reliactyl`
`node index.js`
  
`2. Production`
`cd path/to/the/reliactyl`
`npm install pm2 -g`
`pm2 start index.js`
`pm2 save`

