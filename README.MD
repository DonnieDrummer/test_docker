1. Install Docker
2. Install Docker Compose
3. Clone this project
4. Run `docker-compose build`
5. Go to `src/application` folder, remove `.gitignore` file and clone the app project
    https://github.com/DonnieDrummer/test_app
6. Copy `.env.example` to `.env`
7. If you don't have installed composer locally, run `composer install` inside test.php-fpm container
8. Run migrations and seeds
9. Add row `127.0.0.1 test.vm` to local `/etc/hosts` file  