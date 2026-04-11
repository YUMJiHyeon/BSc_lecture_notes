# TLS Tutorial


## Getting a Domain Name

Either buy a domain name from the registrar of your choice or choose one from those on the list in the [GitHub Education Pack](https://education.github.com/pack) like _Namecheap_, _name.com_, or _.tech domains_.
Then receive a domain name from one of these.

## Setup Nginx

The following is an adapted and abbreviated version of a more comprehensive tutorial from [DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-configure-nginx-as-a-reverse-proxy-on-ubuntu-22-04)

### Installation

```bash
sudo apt update
sudo apt install nginx
```

Check that `nginx` is up and running
```bash
systemctl status nginx
```

### Enable Firewall and Setup Initial Rules

```bash
sudo ufw enable
sudo ufw allow 'Nginx HTTP'
sudo ufw allow ssh
sudo ufw status
```

### Configuring Nginx

The following assumes that your domain is called `your_domain.dk`.

Open an editor to create your new configuration file:

```bash
sudo nano /etc/nginx/sites-available/your_domain.dk
```

and use the following example configuration in it:

```bash
server {
    listen 80;
    listen [::]:80;

    server_name your_domain.dk;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $http_host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        # proxy_http_version 1.1;
        proxy_set_header X-URIScheme https;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}
```

Note, this configuration assumes that you have a locally running webserver listening on port `8080`
After saving the configuration file and after closing the editor, enable the newly created configuration file.
Do so by [symbolically linking](https://www.man7.org/linux/man-pages/man1/ln.1.html) it to the `sites-enabled` directory that Nginx reads at startup:

```bash
sudo ln -s /etc/nginx/sites-available/your_domain.dk /etc/nginx/sites-enabled/
```

Let Nginx double check if it can read your newly created configuration and if it does not contain any obvious errors:

```bash
sudo nginx -t
```

Now, restart Nginx so that it is configured accordingly:

```bash
sudo systemctl restart nginx
```

## Setup and configure a TLS Certificate (http -> https)

### Install `certbot`

Since `certbot` is a Python program, make sure you have a Python interpreter and its dependencies installed on your server
The official documentation is [here](https://certbot.eff.org/instructions?ws=nginx&os=pip).
(An alternative path to installing `certbot` is via Ubuntu `snap`, as e.g., described [in this DigitalOcean tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-22-04). But `snap` is [criticized](https://www.xda-developers.com/you-should-stop-using-snaps-on-ubuntu/) in the open-source world. Therefore, we install it directly.)

```bash
sudo apt update
sudo apt install python3 python3-dev python3-venv libaugeas-dev gcc
```

Set up a [Python virtual environment](https://docs.python.org/3/library/venv.html) for `certbot`

```bash
sudo python3 -m venv /opt/certbot/
sudo /opt/certbot/bin/pip install --upgrade pip
```
Now, finally install `certbot`.

```bash
sudo /opt/certbot/bin/pip install certbot certbot-nginx
```

Create a symbolic link from the just install `certbot` program to a path holding your executables so that you can run it directly as `certbot` command, i.e., by just typing `certbot`.

```bash
sudo ln -s /opt/certbot/bin/certbot /usr/local/bin/certbot
```

### Configure Firewall for TLS

Check firewall status and update it to accept also TLS encrypted, i.e., HTTPS traffic:

```bash
sudo ufw status
sudo ufw allow 'Nginx Full'
sudo ufw delete allow 'Nginx HTTP'
sudo ufw allow ssh
sudo ufw status
```

### Obtaining and Installing a TLS certificate for Your Domain

```bash
sudo certbot --nginx -d your_domain.dk
```

Now, enter your email address, accept terms of service, and a message similar to the following should appear:

```bash
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Enter email address or hit Enter to skip.
 (Enter 'c' to cancel):

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Please read the Terms of Service at:
https://letsencrypt.org/documents/LE-SA-v1.5-February-24-2025.pdf
You must agree in order to register with the ACME server. Do you agree?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing, once your first certificate is successfully issued, to
share your email address with the Electronic Frontier Foundation, a founding
partner of the Let's Encrypt project and the non-profit organization that
develops Certbot? We'd like to send you email about our work encrypting the web,
EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: y
Account registered.
Requesting a certificate for your_domain.dk

Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/your_domain.dk/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/your_domain.dk/privkey.pem
This certificate expires on 2025-07-01.
These files will be updated when the certificate renews.
Certbot has set up a scheduled task to automatically renew this certificate in the background.

Deploying certificate
Successfully deployed certificate for wimblefun.foodeez.dk to /etc/nginx/sites-enabled/your_domain.dk
Congratulations! You have successfully enabled HTTPS on https://your_domain.dk

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
If you like Certbot, please consider supporting our work by:
 * Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate
 * Donating to EFF:                    https://eff.org/donate-le
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
```

### Confirm that TLS Encryption is Working Correctly

Navigate with your browser to https://your_domain.dk/ double check the "lock icon" in front of the URL after loading your page.


### Optional: Automate Renewal of Certificates

TLS certificates expire after a certain period of time.
Thereafter, they have to be renewed.
You can automate this step, e.g., by configuring a CRON job for the task, see step 8 in the [official documentation](https://certbot.eff.org/instructions?ws=nginx&os=pip).