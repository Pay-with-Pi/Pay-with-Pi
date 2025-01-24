# Pi Platform Demo App: Development Environment

The following document explains how to set up a development environment and run the Pi Platform Demo App in the
sandbox environment.

## Prerequisites:

This guides assumes you have the following two tools installed on your development machine:

- a NodeJS installation (recommended version: Node v16 LTS **or lower**)
  - if you're running with node 17 or higher, you'll need to use `yarn startNode17` to work around [this issue](https://github.com/facebook/create-react-app/issues/11562)
- a functional Docker or Mongosh installation


## 1. Clone the Github repo and navigate to the project directory:

```sh
git clone git@github.com:pi-apps/platform-demo-app.git
cd platform-demo-app
```


## 2. Register your app on the developer portal

Open `develop.pi` in the Pi Browser, on your mobile phone, and go through the prerequisite steps
(e.g verifying your email address).

Create a new app by clicking the "Register an App" button.

The Process is as follows:

- Register an App:
  - Name: The name of your app
  - Description: A public user-facing description of your app
  - Network: select "Pi Testnet"
  - Submit the form

<img title="Register An App" alt="Registration Form for an App" src="./img/register_app.PNG" style="width:300px;height:600px;" />

<br/>

This will bring you to the App Dashboard, from this screen you can continue the development of the demo app. 
 
- App Checklist: Complete Steps 1-5 to prepare the app for launch in development mode
  - Step 1: "Register an App" was completed previously
  - Step 2: Configure App Hosting - Hosting type: select "Self hosted"
  - Step 3: Create a Pi Wallet, see this [Pi Wallet Introduction](https://pi-apps.github.io/community-developer-guide/docs/importantTopics/paymentFlow/piWallet/) for more information
  - Step 4: Review this documentation and our [Community Developer Guide](https://pi-apps.github.io/community-developer-guide/) for help getting setup
  - Step 5: Configure App Development URL: the URL on which your app is running on your development environment. If your using the default
    setup for the demo app frontend, this is "http://localhost:3314. **Note:** If you need, you can change the port by specifying it in
    `frontend/.env` file, as the value of the `PORT` environment variable.
 
 <img title="Developer Portal App Checklist" alt="App Checklist" src="./img/app_checklist.png" style="width:300px;height:1100px;" />
 
 <br/>
 
- App Configuration: Additional information that can be adjusted
  - Whitelisted usernames: you can leave this blank at this point
  - App URL: This is irrelevant for development. You can use the intended production URL of your app (e.g "https://mydemoapp.com"),
    or simply set it up to an example value (e.g "https://example.com"). This must be an HTTPs URL
  - Development URL: The URL on which your app is running on your development environment. If your using the default
    setup for the demo 

## 3. Run the frontend development server

Setup the frontend app following the [Pi Demo App Frontend documentation](../frontend/README.md).


## 4. Run the backend development server

Setup backend server following the [Pi Demo App Backend documentation](../backend/README.md).

## 5. Open the app in the Sandbox

To test all of the Demo App features, you need to run it in the Pi Sandbox.

The purpose of the Sandbox is to enable running and debugging a Pi App in a desktop browser, although a Pi App
is meant to be opened in the Pi Browser by end-users.

For more information on the Sandbox head to our [Community Developer Guide](https://pi-apps.github.io/community-developer-guide/docs/gettingStarted/piAppPlatform/piAppPlatformSDK/#the-sandbox-flag).

Lastly, **on your desktop browser** open the sandbox URL from Step 6 of App Checklist:

![Sandbox URL](./img/sandbox_url.png)

![Sandbox URL](./img/sandbox_firefox.png)

> **WARNING**
>
> The demo app uses express session cookies which, in the Sandbox environment, are not correctly saved on the client on some browsers.
> To properly test all of the features of the Demo App, we recommend you to open the sandbox app using Mozilla Firefox.

#### Congratulations! The app should work in the developer portal and enable you to sign in, place an order and make a testnet payment.

# More Information - Developing on Pi
For guidelines on how to register an app and get the Sandbox URL, please refer to the
[Pi Developer Guide](https://pi-apps.github.io/community-developer-guide/).

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

### Installing Mongoose

To install Mongoose, run the following command:

```sh
yarn add mongoose
```

### Setting Up Mongoose Connection

To set up the Mongoose connection, add the following code to your backend server file (e.g., `server.js`):

```javascript
const mongoose = require('mongoose');

const mongoDB = process.env.MONGODB_URI || 'mongodb://localhost:27017/Pay with Piapp-development';

mongoose.connect(mongoDB, { useNewUrlParser: true, useUnifiedTopology: true })
  .then(() => console.log('Connected to MongoDB via Mongoose'))
  .catch((err) => console.error('MongoDB connection error:', err));
```
