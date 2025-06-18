
[![Youtube][youtube-shield]][youtube-url]
[![Facebook][facebook-shield]][facebook-url]
[![Instagram][instagram-shield]][instagram-url]
[![LinkedIn][linkedin-shield]][linkedin-url]

Thanks for visiting my GitHub account!

# Laravel Project Setup Guide in WSL (Ubuntu) with (Apache + MySQL + phpMyAdmin + Redis)

> A complete step-by-step setup of the ALTERC Laravel project on **WSL (Ubuntu)** using Apache, MySQL, phpMyAdmin, and optional Redis. It is structured for practical future reference.


## Table of Contents

0. [System Requirements](#system-requirements)
1. [WSL & Ubuntu Setup](#1-wsl--ubuntu-setup)
2. [Apache Web Server Configuration](#2-apache-web-server-configuration)
3. [MySQL Setup & Root Access Fix](#3-mysql-setup--root-access-fix)
4. [phpMyAdmin Configuration](#4-phpmyadmin-configuration)
5. [Redis (Optional)](#5-redis-optional)
6. [Laravel Project Setup](#6-laravel-project-setup)
7. [Vite & NPM](#7-vite--npm)
8. [Launch the Project](#8-launch-the-project)
9. [Access from Browser](#9-access-from-browser)
10. [Common Commands](#10-common-commands)
11. [Troubleshooting](#11-troubleshooting)

---

## 0. System Requirements

- Windows 10/11 with WSL2 enabled
- Ubuntu via WSL
- Node.js (18.x LTS preferred)
- PHP 8.1+
- MySQL (inside WSL)
- Apache2 (inside WSL)
- phpMyAdmin (inside WSL)

---

## 1. WSL Installation & Ubuntu Setup

- Open terminal (command prompt) and run 

```bash
wsl --install
```

Launch Ubuntu terminal by search ubuntu in search bar and set up your user.

---

#### Installing Dependencies
- Open Ubuntu Terminal.

```bash
sudo apt update && sudo apt upgrade
sudo apt install php php-mysql php-xml php-mbstring php-curl unzip curl mysql-server apache2 phpmyadmin npm nodejs
```

## 2. Apache Web Server Configuration

```bash
sudo apt install apache2 -y
sudo service apache2 restart
```

To restart manually:
```bash
sudo service apache2 restart
```

## 3. MySQL Setup & Root Access Fix

```bash
sudo apt install mysql-server -y
sudo service mysql start
```

To login securely:
```bash
sudo mysql
```

Then run:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '12345678';
FLUSH PRIVILEGES;
EXIT;
```

Now you can log in normally:

```bash
mysql -u root -p
# Password: 12345678
```

Create a new user for phpMyAdmin:

```sql
CREATE USER IF NOT EXISTS 'phpmyadmin'@'localhost' IDENTIFIED BY '12345678';
GRANT ALL PRIVILEGES ON *.* TO 'phpmyadmin'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
EXIT;
```

## 4. phpMyAdmin Configuration

```bash
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
sudo phpenmod mbstring
sudo service apache2 restart
```

Enable phpMyAdmin in Apache:

```bash
sudo ln -s /etc/phpmyadmin/apache.conf /etc/apache2/conf-available/phpmyadmin.conf
sudo a2enconf phpmyadmin
sudo service apache2 restart
```

Access: [http://localhost/phpmyadmin](http://localhost/phpmyadmin)

## 5. Redis (Optional)

```bash
sudo apt install redis-server -y
sudo service redis-server start
```

- Then test Redis:

```bash
redis-cli ping
```
- Expected output:
```bash
PONG
```

- Test Redis connection from Laravel:

```bash
php artisan cache:clear
```


## 6. Laravel Project Setup

Cloning or Copying Project:

```bash
cd ~
git clone https://your-repo-link.git alterc
cd alterc
```

Or if already placed:

```bash
cd ~/alterc
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
```

---

#### Open Source code in VS code

```bash
cd ~/alterc
code .
```



#### Accessing Project Files from Windows

In WSL:
```bash
explorer.exe .
```

Or from Windows:
```
\\\\wsl.localhost\\Ubuntu\\home\\learnwithfair\\alterc
```

---

Make `.env` changes:

```
DB_DATABASE=alterc
DB_USERNAME=phpmyadmin
DB_PASSWORD=12345678
```

## 7. Vite & NPM

Inside the Laravel project:

**Terminal 1:**

```bash
rm -rf node_modules package-lock.json
npm install --legacy-peer-deps
npm run dev
```

---

#### Vite Development Server

- `npm run dev` for development.
- `npm run build` for production build.


## 8. Launch the Project (Custom domain)

**Terminal 2:**

```bash
php artisan serve --host=superadmin.trekntread.com --port=8000
```

You may add to `/etc/hosts`: (Custom domain)

```bash
127.0.0.1 superadmin.trekntread.com
```

## 9. Access from Browser

Visit: [http://superadmin.trekntread.com:8000](http://superadmin.trekntread.com:8000)

If redirected to HTTPS, check Laravel `.env`:

```
APP_URL=http://superadmin.trekntread.com:8000
```
And **clear config cache**:

```bash
php artisan config:clear
php artisan cache:clear
```

## 10. Common Commands

| Action                     | Command                             |
|---------------------------|--------------------------------------|
| Restart Apache            | `sudo service apache2 restart`       |
| Stop Apache               | `sudo service apache2 stop`          |
| Start MySQL               | `sudo service mysql start`           |
| Stop MySQL                | `sudo service mysql start`           |
| Start Redis Server        | `sudo service redis-server stop`     |
| Stop Redis Server         | `sudo service redis-server stop`     |
| Laravel migration         | `php artisan migrate --seed`         |
| Clear config/cache        | `php artisan config:clear && php artisan cache:clear` |
| Start dev server (vite)   | `npm run dev`                        |
| Start Laravel server      | `php artisan serve`                  |

## 11. Troubleshooting

- **NPM Error UNC paths**: Ensure you're not running `npm` commands from a Windows CMD if using WSL. Always use Ubuntu terminal.
- **Redis error**: If not used, disable Redis config or install Redis as shown.
- **Port Conflicts**: Use different ports or stop conflicting services (like XAMPP/Apache).

---


**✅ All done. Your Laravel + Vite project is now fully configured in WSL with Apache2, MySQL, and phpMyAdmin support.**


## Follow Me

[<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/github.svg' alt='github' height='40'>](https://github.com/learnwithfair) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/facebook.svg' alt='facebook' height='40'>](https://www.facebook.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/instagram.svg' alt='instagram' height='40'>](https://www.instagram.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/twitter.svg' alt='twitter' height='40'>](https://www.twiter.com/learnwithfair/) [<img src='https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/youtube.svg' alt='YouTube' height='40'>](https://www.youtube.com/@learnwithfair)

<!-- MARKDOWN LINKS & IMAGES -->

[youtube-shield]: https://img.shields.io/badge/-Youtube-black.svg?style=flat-square&logo=youtube&color=555&logoColor=white
[youtube-url]: https://youtube.com/@learnwithfair
[facebook-shield]: https://img.shields.io/badge/-Facebook-black.svg?style=flat-square&logo=facebook&color=555&logoColor=white
[facebook-url]: https://facebook.com/learnwithfair
[instagram-shield]: https://img.shields.io/badge/-Instagram-black.svg?style=flat-square&logo=instagram&color=555&logoColor=white
[instagram-url]: https://instagram.com/learnwithfair
[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=flat-square&logo=linkedin&colorB=555
[linkedin-url]: https://www.linkedin.com/in/rahatul-rabbi/

