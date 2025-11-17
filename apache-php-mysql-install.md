
```bash
#!/usr/bin/env bash

# Simple LAMP Installer
# Installs Apache, MySQL, PHP, and common PHP extensions
# Works on Ubuntu/Debian systems

set -e

if [ "$EUID" -ne 0 ]; then
  echo "Please run as root (sudo bash $0)"
  exit 1
fi

echo "Updating system..."
apt update -y

echo "Installing Apache..."
apt install -y apache2

echo "Installing MySQL Server..."
DEBIAN_FRONTEND=noninteractive apt install -y mysql-server

echo "Installing PHP and common extensions..."
apt install -y \
  php \
  libapache2-mod-php \
  php-cli \
  php-mysql \
  php-mbstring \
  php-xml \
  php-curl \
  php-gd \
  php-zip \
  php-intl \
  php-bcmath \
  php-json

echo "Enabling Apache modules..."
a2enmod php* || true
a2enmod rewrite

echo "Restarting Apache..."
systemctl restart apache2

echo "------------------------------------------"
echo "LAMP Install Complete!"
echo
echo "Apache: Installed"
echo "MySQL : Installed (run mysql_secure_installation manually)"
echo "PHP   : Installed with common extensions"
echo
echo "To test PHP, run:"
echo "  echo \"<?php phpinfo(); ?>\" > /var/www/html/info.php"
echo "Then open: http://YOUR_SERVER_IP/info.php"
echo "------------------------------------------"

'''

### Install Script

'''bash
nano install-lamp.sh
'''
Paste the script → save → exit.

Make it executable:
'''bash
chmod +x install-lamp.sh
'''

Run:
'''bash
sudo ./install-lamp.sh
'''
