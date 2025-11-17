
# Creates new admin user 'w38g0ru' and disables old 'root'

``` bash
set -e

# New admin username + password
NEW_USER="w38g0ru"
NEW_PASS="root"   # change this to a strong password!

echo "[*] Securing MySQL and replacing root user..."

# Create new superuser
mysql -e "CREATE USER '${NEW_USER}'@'localhost' IDENTIFIED WITH mysql_native_password BY '${NEW_PASS}';"
mysql -e "GRANT ALL PRIVILEGES ON *.* TO '${NEW_USER}'@'localhost' WITH GRANT OPTION;"

# Remove anonymous users
mysql -e "DELETE FROM mysql.user WHERE User='';"

# Remove old root user
mysql -e "DROP USER IF EXISTS 'root'@'localhost';"

# Remove test database
mysql -e "DROP DATABASE IF EXISTS test;"
mysql -e "DELETE FROM mysql.db WHERE Db='test' OR Db='test_%';"

# Apply changes
mysql -e "FLUSH PRIVILEGES;"

echo "[OK] MySQL secured."
echo "New admin user: ${NEW_USER}"
echo "Password: ${NEW_PASS}"
echo "Old root account removed."


#!/usr/bin/env bash
#
# Secure MySQL installation
# Creates new admin user 'w38g0ru' and disables old 'root'
#

set -e

# New admin username + password
NEW_USER="w38g0ru"
NEW_PASS="root"   # change this to a strong password!

echo "[*] Securing MySQL and replacing root user..."

# Create new superuser
mysql -e "CREATE USER '${NEW_USER}'@'localhost' IDENTIFIED WITH mysql_native_password BY '${NEW_PASS}';"
mysql -e "GRANT ALL PRIVILEGES ON *.* TO '${NEW_USER}'@'localhost' WITH GRANT OPTION;"

# Remove anonymous users
mysql -e "DELETE FROM mysql.user WHERE User='';"

# Remove old root user
mysql -e "DROP USER IF EXISTS 'root'@'localhost';"

# Remove test database
mysql -e "DROP DATABASE IF EXISTS test;"
mysql -e "DELETE FROM mysql.db WHERE Db='test' OR Db='test_%';"

# Apply changes
mysql -e "FLUSH PRIVILEGES;"

echo "[OK] MySQL secured."
echo "New admin user: ${NEW_USER}"
echo "Password: ${NEW_PASS}"
echo "Old root account removed."
```
### Installation

✔ How to Use
'''bash
nano secure-mysql.sh
'''

Paste → save → exit.

Make executable:

chmod +x secure-mysql.sh


Run:

sudo ./secure-mysql.sh
