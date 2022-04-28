# Apache config for Redhat and Debian

**Install Apache** ➡️ *yum install httpd*

**Install ssl for certs** ➡️ *yum install mod_ssl*

**Create a soft link** ➡️ *ln -s /etc/pki/tls/private private*

**Create your cert and key and place it on here** ⬇️

*/etc/ssl/certs/* - **(For certificate)**

*/etc/ssl/private/* - **(For key)** 🔖 **If you dont have this folder just create it** 🔖

**Copy the html folder and make the htmls folder for the https page** ⬇️

*cp -r /var/www/html /var/www/htmls*

**Go to /etc/httpd/conf.d/ssl.conf**

**Uncomment and edit for your settings** ⬇️

*DocumentRoot "/var/www/htmls"

*ServerName hostname:443*

**Comment** ⬇️

*#SSLProtocol all -SSLv3*

*#SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5:!SEED:!IDEA*

**Edit your cert and key** ⬇️
```
*SSLCertificateFile /etc/ssl/certs/crt.crt*
 
*SSLCertificateKeyFile /etc/ssl/private/key.key*
 ```
 
**systemctl restart httpd**


**For Debian**

apt install apache2

To activate HTTPS
```
a2enmod ssl
a2ensite default-ssl.conf
systemctl restart apache2
```
**Change some settings and create a second dir**
```
cd /etc/apache2/sites-available/
nano default-ssl.conf
Change the doc from /var/www/html to /var/www/htmls
cd /var/www
cp -R html/ htmls
nano /etc/apache2/sites-available/default-ssl.conf
e modificar os ssl primeiro é (yourcert.crt and second yourkey.key
cd /etc/ssl/certs
cp /etc/easy-rsa/pki/private/*.crt .
cd ../private/
cp /etc/easy-rsa/pki/private/*.key .
chown --reference=ssl-cert-snakeoil.key *pt.key
chmod --reference=ssl-cert-snakeoil.key *pt.key
systemctl restart apache2
