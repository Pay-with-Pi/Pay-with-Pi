# Pay with Pi

## Introduction
Use Pay with Pi for the fastest, most secure online and in-store payments! Pay for movie tickets, food, coffee, fashion, gas, and many more in Pay with Pi. Quick, easy, convenient, and secure.

## Send/Receive Payment
Pay in store or send money to friends. No need to carry cash or worry about loose change!

- **Online Top-Ups and Utility Bill Payments**: Top-up your mobile phone, pay your utility and internet bills or settle your monthly insurance premiums bills through Pay with Pi.
- **Add Money to your Pay with Pi Wallet**: Add money to your Pay with Pi app via Pay&Go machines or transfer from multiple online banking apps, or cash-in at all Bank branches and agents worldwide.
- **Explore Nearby**: Explore places near you that accept payment through Pay with Pi wallet. Cinemas, restaurants, coffee shops, supermarkets, and gas stations are all joining forces with Pay with Pi to make your life more connected and more mobile.

## Apache2, MySQL, and PHP Setup Instructions

### Installing Apache2, MySQL, and PHP

To install Apache2, MySQL, and PHP, run the following commands:

```sh
sudo apt-get update
sudo apt-get install apache2
sudo apt-get install mysql-server
sudo apt-get install php libapache2-mod-php php-mysql
```

### Configuring Apache2 to Serve `index.html`

1. Create a new configuration file for your website:

```sh
sudo nano /etc/apache2/sites-available/my-website.conf
```

2. Add the following content to the configuration file:

```sh
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /my-website/public

    <Directory /my-website/public>
        Options Indexes FollowSymLinks
        AllowOverride None
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

3. Enable the new site and reload Apache2:

```sh
sudo a2ensite my-website.conf
sudo systemctl reload apache2
```

### Setting Up MySQL Database and User

1. Log in to the MySQL root account:

```sh
sudo mysql -u root -p
```

2. Create a new database and user:

```sql
CREATE DATABASE my_database;
CREATE USER 'my_user'@'localhost' IDENTIFIED BY 'my_password';
GRANT ALL PRIVILEGES ON my_database.* TO 'my_user'@'localhost';
FLUSH PRIVILEGES;
EXIT;
```

### Configuring PHP with Necessary Modules

1. Open the PHP configuration file:

```sh
sudo nano /etc/php/7.4/apache2/php.ini
```

2. Ensure the following modules are enabled:

```ini
extension=mysqli
extension=pdo_mysql
```

3. Restart Apache2 to apply the changes:

```sh
sudo systemctl restart apache2
```

## Conclusion
Don’t forget to look out for great deals exclusively for Pay with Pi users! Start enjoying the amazing benefits of Pay with Pi. Download it now.

[Download Pay with Pi](https://forms.gle/NBzpicuQ1SXQSH4e6)
