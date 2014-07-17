## Setup the Continuous Deployment Server

* SSH into strider box ssh://deploy@strider.knban.com

* Install Strider-CD from source with ssh deploy plugin

```
cd /home/deploy
git clone https://github.com/Strider-CD/strider.git
cd strider
npm install --production
npm install strider-ssh-deploy
bin/strider addUser
```

* Add supervisor configuration

```
cat <<-EOF | sudo tee /etc/supervisor/conf.d/strider.conf
[program:strider]
command=/home/deploy/strider/bin/strider
stdout_logfile=/var/log/supervisor/%(program_name)s.log
redirect_stderr=true
autorestart=true
user=deploy
stopasgroup=true
environment=HOME="/home/deploy"
environment=NODE_ENV="production"
environment=SERVER_NAME="https://strider.knban.com"
environment=PLUGIN_GITHUB_APP_ID="8c1369903974542b168e"
environment=PLUGIN_GITHUB_APP_SECRET="f952aeb15ca52f079a6e5f77c211670b590f2a05"
environment=SMTP_HOST="localhost"
environment=SMTP_PORT=25
environment=SMTP_USER=""
environment=SMTP_PASS=""
environment=SMTP_FROM="Strider no-reply@strider.knban.com"
environment=PORT=3000
EOF

sudo supervisorctl reread
sudo supervisorctl update
```

* Add nginx configuration

```
cat <<-EOF | sudo tee /etc/nginx/sites-available/strider
server {
  listen      80;
  return 301 https://\$http_host:443\$request_uri;
}

server {
  listen 443;
  server_name strider.knban.com;
  ssl on;
  ssl_certificate /var/ssl/star_knban_com.pem;
  ssl_certificate_key /var/ssl/star_knban_com.key;

  location / {
    proxy_set_header X-Forwarded-For \$proxy_add_x_forwarded_for;
    proxy_set_header Host \$http_host;
    proxy_redirect off;
    proxy_pass http://127.0.0.1:3000;
  }
}
EOF

sudo ln -s /etc/nginx/sites-available/strider /etc/nginx/sites-enabled/strider
sudo service nginx reload
```

* Go to https://strider.knban.com
