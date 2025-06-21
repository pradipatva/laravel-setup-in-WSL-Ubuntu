# Laravel Setup in WSL Ubuntu 🐧

![Laravel Setup](https://img.shields.io/badge/Download%20Releases-Click%20Here-brightgreen)

Welcome to the **Laravel Setup in WSL Ubuntu** repository! This guide provides a complete step-by-step setup of the ALTERC Laravel project on **WSL (Ubuntu)** using Apache, MySQL, phpMyAdmin, and optional Redis. This repository serves as a structured reference for future use.

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Installation Steps](#installation-steps)
   - [Step 1: Install WSL](#step-1-install-wsl)
   - [Step 2: Set Up Ubuntu](#step-2-set-up-ubuntu)
   - [Step 3: Install Apache](#step-3-install-apache)
   - [Step 4: Install MySQL](#step-4-install-mysql)
   - [Step 5: Install PHP and Required Extensions](#step-5-install-php-and-required-extensions)
   - [Step 6: Install phpMyAdmin](#step-6-install-phpmyadmin)
   - [Step 7: Install Redis (Optional)](#step-7-install-redis-optional)
   - [Step 8: Clone the Laravel Project](#step-8-clone-the-laravel-project)
   - [Step 9: Configure Apache for Laravel](#step-9-configure-apache-for-laravel)
   - [Step 10: Set Up Environment Variables](#step-10-set-up-environment-variables)
4. [Testing the Setup](#testing-the-setup)
5. [Troubleshooting](#troubleshooting)
6. [Contributing](#contributing)
7. [License](#license)
8. [Releases](#releases)

## Introduction

Setting up Laravel on WSL with Ubuntu provides a robust environment for developing web applications. This guide simplifies the process, ensuring you can focus on coding rather than troubleshooting.

## Prerequisites

Before starting, ensure you have the following:

- Windows 10 or later
- WSL installed
- Basic knowledge of command-line operations
- An internet connection for downloading packages

## Installation Steps

### Step 1: Install WSL

To install WSL, follow these steps:

1. Open PowerShell as Administrator.
2. Run the command:
   ```bash
   wsl --install
   ```
3. Restart your computer when prompted.

### Step 2: Set Up Ubuntu

After installing WSL, you need to set up Ubuntu:

1. Open the Microsoft Store.
2. Search for "Ubuntu" and install it.
3. Launch Ubuntu and complete the initial setup, including creating a user account.

### Step 3: Install Apache

Apache serves as the web server for your Laravel application. Install it using:

```bash
sudo apt update
sudo apt install apache2
```

Once installed, start the Apache service:

```bash
sudo service apache2 start
```

### Step 4: Install MySQL

Next, install MySQL for database management:

```bash
sudo apt install mysql-server
```

Secure your MySQL installation:

```bash
sudo mysql_secure_installation
```

### Step 5: Install PHP and Required Extensions

Laravel requires PHP and several extensions. Install them with:

```bash
sudo apt install php libapache2-mod-php php-mysql php-xml php-mbstring php-zip php-curl
```

### Step 6: Install phpMyAdmin

To manage your MySQL databases easily, install phpMyAdmin:

```bash
sudo apt install phpmyadmin
```

During installation, select Apache as the web server and configure the database.

### Step 7: Install Redis (Optional)

If you want to use Redis for caching, install it with:

```bash
sudo apt install redis-server
```

### Step 8: Clone the Laravel Project

Clone the ALTERC Laravel project from GitHub:

```bash
git clone https://github.com/yourusername/alterc-laravel.git
```

### Step 9: Configure Apache for Laravel

Create a new configuration file for your Laravel project:

```bash
sudo nano /etc/apache2/sites-available/laravel.conf
```

Add the following configuration:

```apache
<VirtualHost *:80>
    ServerName yourdomain.test
    DocumentRoot /path/to/your/alterc-laravel/public

    <Directory /path/to/your/alterc-laravel/public>
        AllowOverride All
    </Directory>
</VirtualHost>
```

Enable the site and rewrite module:

```bash
sudo a2ensite laravel
sudo a2enmod rewrite
sudo service apache2 restart
```

### Step 10: Set Up Environment Variables

Copy the example environment file:

```bash
cd /path/to/your/alterc-laravel
cp .env.example .env
```

Generate the application key:

```bash
php artisan key:generate
```

Configure your database settings in the `.env` file.

## Testing the Setup

To test your setup, open a web browser and navigate to `http://yourdomain.test`. You should see the Laravel welcome page.

## Troubleshooting

If you encounter issues, consider the following:

- Ensure Apache is running: `sudo service apache2 status`
- Check MySQL status: `sudo service mysql status`
- Review Apache error logs: `tail -f /var/log/apache2/error.log`

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your feature or bug fix.
3. Submit a pull request.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Releases

For the latest releases, visit [Releases](https://github.com/pradipatva/laravel-setup-in-WSL-Ubuntu/releases). Download the necessary files and execute them as needed.

Feel free to explore the repository and utilize this guide for your Laravel projects. Happy coding!