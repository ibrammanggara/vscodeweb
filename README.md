#### installl
```
curl -fsSL https://code-server.dev/install.sh | sh
```

## cek password
```
/root/.config/code-server/config.yaml 
```
## install require apache2
```
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_wstunnel
sudo a2enmod rewrite
```
## proxy to domain vscode
```
<VirtualHost *:80>
    ServerName {yourdomain.site}

    ProxyPass / http://localhost:8080/
    ProxyPassReverse / http://localhost:8080/

    ProxyPass /ws/ ws://localhost:8080/ws/
    ProxyPassReverse /ws/ ws://localhost:8080/ws/

    RewriteEngine On

    # Rewrite untuk WebSocket
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteCond %{HTTP:Connection} upgrade [NC]
    RewriteRule /(.*) ws://localhost:8080/$1 [P,L]


    ErrorLog ${APACHE_LOG_DIR}/yourdomain-error.log
    CustomLog ${APACHE_LOG_DIR}/yourdomain-access.log combined
</VirtualHost>
```
