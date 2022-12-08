# Deploying a Django application in VM

For development server we can use the built-in Django server. But for production we need to use a web server like Apache or Nginx. In this tutorial we will use Nginx.

* For safety create a new production branch in git and push it to the server.
```git
git branch prod
git checkout prod
git push origin prod
```
* Now we have to install gunicorn then we can call it directly
```bash
pip install gunicorn
```
* Our project have a wsgi.py file, so we can directly start wsgi server 
```bash
cd backend/anwesha
gunicorn anwesha.asgi
```
* We have some pending configuration in wsgi server, but lets setup nginx first
```bash
sudo apt-get install nginx
```
* Now we have to configure nginx to serve our application. We will use a reverse proxy to serve our application. We will use a file named `anwesha.conf` in `/etc/nginx/sites-available/` directory. This file will contain the following configuration
```nginx
server {
    listen 80;
    server_name backend.anwesha.live;
    location / {
        proxy_pass http://127.0.0.1:8000;
    }
}
```
* Now we have to enable this configuration by creating a symbolic link in `/etc/nginx/sites-enabled/` directory
```bash
sudo ln -s /etc/nginx/sites-available/anwesha.conf /etc/nginx/sites-enabled
```

* Now we have to restart nginx server
```bash
sudo systemctl restart nginx
```
* Now we have a reverse proxy that serves forwards all request at port 80 to port 8000

* Before moving to wsgi configuration, lets setup ssl certificate with letsencrypt. We will use certbot to generate ssl certificate. We will use nginx plugin to generate certificate.
```bash
sudo apt-get install certbot python3-certbot-nginx
```
* Now we have to generate certificate
```bash
sudo certbot --nginx -d backend.anwesha.live
```
* we should add it to crontab to renew certificate automatically
```bash
sudo crontab -e
```
* Add the following line to crontab
```bash
0 0 * * * /usr/bin/certbot renew --quiet
```
* Now that our server is running fine, we have some pending configuration in wsgi server. We have to configure gunicorn to serve our application. I am keeping the filename as `./conf/gunicorn.conf.py` and it is in the same directory as `manage.py`.

```python
wsgi_app = 'anwesha.wsgi'
bind = '0.0.0.0:8000'
workers = 4
loglevel = "debug"
keep-alive = 60
threads = 4
pid = './conf/gunicorn.pid'
access-logfile = './conf/gunicorn-access.log'
capture_output = True
```
* We can demonize and run in background, but for this case i'll run in screen terminal.
* Now we are ready to start our server with gunicorn as deamon
```bash
gunicorn -c ./conf/gunicorn.conf.py
```
* Push the prod branch. 



