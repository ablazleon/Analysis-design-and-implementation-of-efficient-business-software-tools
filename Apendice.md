# Apéndice

## 1. Instalación de odoo en vm

https://www.odoo.com/documentation/14.0/setup/install.html
https://www.youtube.com/watch?v=ud0z9GB6phs
https://www.cybrosys.com/blog/how-to-install-odoo-14-on-ubuntu-20-04-lts

=> change the contorl form vmsgq to the otehr and hten autoresize

```
sudo apt-get update

sudo apt-get upgrade -y

sudo apt-get install openssh-server fail2ban -y

sudo adduser --system --home=/opt/odoo --group odoo

sudo apt-get install -y python3-pip

sudo apt-get install python-dev python3-dev libxml2-dev libxslt1-dev zlib1g-dev libsasl2-dev libldap2-dev build-essential libssl-dev libffi-dev libmysqlclient-dev libjpeg-dev libpq-dev libjpeg8-dev liblcms2-dev libblas-dev libatlas-base-dev 

sudo apt-get install -y npm
sudo ln -s /usr/bin/nodejs /usr/bin/node
sudo npm install -g less less-plugin-clean-css
sudo apt-get install -y node-less

sudo apt-get install postgresql -y

sudo su - postgres
createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo14

psql
ALTER USER odoo14 WITH SUPERUSER;

\q
exit

sudo apt-get install git -y

sudo su - odooUser -s /bin/bash

git clone https://www.github.com/odoo/odoo --depth 1 --branch 14.0 --single-branch .

exit

sudo pip3 install -r /opt/odoo/requirements.txt

sudo wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb
sudo dpkg -i wkhtmltox_0.12.5-1.bionic_amd64.deb
sudo apt install -f

-----------------

sudo cp /opt/odoo/debian/odoo.conf /etc/odoo.conf
sudo nano /etc/odoo.conf

sudo chown odooUser: /etc/odoo.conf
sudo chmod 640 /etc/odoo.conf

sudo mkdir /var/log/odoo
sudo chown odooUser:root /var/log/odoo

sudo nano /etc/systemd/system/odoo.service

sudo chmod 755 /etc/systemd/system/odoo.service
sudo chown root: /etc/systemd/system/odoo.service

sudo systemctl start odoo.service
sudo systemctl status odoo.service

---------------

sudo apt install postgresql -y

wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
echo "deb http://nightly.odoo.com/14.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list
apt-get update && apt-get install odoo

```

