# Lavarelapp Installation
## Deploying a lavarel app in ec2 instance with LAMP

### Prerequisites:
- Amazon EC2 Instance:
- AWS Account

Launch an EC2 instance with an appropriate configuration (e.g., Ubuntu).
Ensure that the security group associated with the EC2 instance allows traffic on ports 80 and 22.
Connect to EC2 Instance:

Use SSH to connect to your EC2 instance. 
For example:
```
ssh -i /path/to/your/key.pem ubuntu@your-ec2-instance-ip
```
LAMP Stack or Nginx/PHP-FPM:
Install a web server (Apache or Nginx) and PHP on your EC2 instance.

Composer:
Install Composer on your EC2 instance. Composer is a dependency manager for PHP.
```
sudo apt update
sudo apt install php-cli unzip
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
php -r "if (hash_file('sha384', 'composer-setup.php') === 'YOUR_SHA384_HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
sudo php composer-setup.php --install-dir=/usr/local/bin --filename=composer
php -r "unlink('composer-setup.php');"
```
Deploy Laravel App:
Clone the Repository:

Clone the Laravel app repository to your EC2 instance:
```
git clone https://github.com/radvc/laravel-blog-api-hands-on.git
```
Install Dependencies:

Navigate to the project directory and install dependencies using Composer:
```
cd laravel-blog-api-hands-on
composer install
```
Configure Environment Variables:

Copy the .env.example file to a new file named .env:
```
cp .env.example .env
```
Edit the .env file with your database credentials and other necessary configurations.

Generate Application Key:

Generate the Laravel application key:
```
php artisan key:generate
```

Run Migrations and Seed Database:
Run database migrations and seed the database:
```
php artisan migrate --seed
```

Configure Web Server:
If you're using Apache, configure the virtual host. If you're using Nginx, create a server block.

For Apache:
```
sudo nano /etc/apache2/sites-available/your-site.conf
```
For Nginx:
```
sudo nano /etc/nginx/sites-available/your-site
```
Configure the virtual host or server block to point to the Laravel public directory.
Enable Site and Restart Server:

Enable the site (for Apache) and restart the web server:
For Apache:
```
sudo a2ensite your-site.conf
sudo service apache2 restart
```
For Nginx:
```
sudo ln -s /etc/nginx/sites-available/your-site /etc/nginx/sites-enabled
sudo service nginx restart
```
Set Appropriate Permissions:
Ensure that the storage and bootstrap/cache directories are writable:
```
sudo chmod -R 775 storage bootstrap/cache
```
Access Your Laravel App:
Open your browser and navigate to your EC2 instance's public IP or domain name to access the Laravel app.
