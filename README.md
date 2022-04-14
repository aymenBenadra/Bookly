# Bookly - Sell or Buy books online

Bookly is an anoucement site for books which allows you to sell or buy books online.

## Pages

- [ ] Authentication page
- [ ] Offers page
- [ ] Demands page
- [ ] Admin Dashboard page (*Bonus*⭐)

## Definitions

- **Laravel** [https://laravel.com/](https://laravel.com/): is a free, open-source PHP web framework, created by Taylor Otwell and intended for the development of web applications following the model–view–controller (MVC) architectural pattern and based on Symfony.
- **PHP Artisan** [https://laravel.com/docs/9.x/artisan](https://laravel.com/docs/9.x/artisan): is a command line interface for the [Laravel Framework](https://laravel.com/) that makes it easy to execute tasks and perform various developer tasks.
- **Composer** [https://getcomposer.org/](https://getcomposer.org/): is a package manager for PHP that allows you to install and manage dependencies of your PHP application.
- **ORM** [https://laravel.com/docs/9.x/eloquent](https://laravel.com/docs/9.x/eloquent): is a database query builder and **Eloquent** is an ORM for the [Laravel Framework](https://laravel.com/) that provides a simple, expressive API for defining relationships between your models, accessing the underlying database, and performing basic data validation.
- **Migration** [https://laravel.com/docs/9.x/migrations](https://laravel.com/docs/9.x/migrations): is a database migration tool for the [Laravel Framework](https://laravel.com/) that allows you to create, modify, and delete tables and columns in your database using a simple, expressive language.
- **Blade** [https://laravel.com/docs/9.x/blade](https://laravel.com/docs/9.x/blade): is a template language for the [Laravel Framework](https://laravel.com/) that makes it easy to generate HTML views using PHP.

### Use case diagram

![PNG version](modelization/Use%20case%20diagram.png)

[PDF version](modelization/Use%20case%20diagram.pdf)

### Class diagram

![PNG version](modelization/Class%20diagram.png)

[PDF version](modelization/Class%20diagram.pdf)

## SQL Queries

1. Creating Database:

    ```sql
    CREATE DATABASE IF NOT EXISTS `bookly`;
    ```

2. Using Database:

    ```sql
    USE `bookly`;
    ```

3. Creating Tables:
    1. Users:

        ```sql
        CREATE TABLE IF NOT EXISTS `users` (
            `id` int(11) NOT NULL AUTO_INCREMENT,
            `first_name` varchar(255) NOT NULL,
            `last_name` varchar(255) NOT NULL,
            `email` varchar(255) NOT NULL,
            `password` varchar(255) NOT NULL,
            `is_admin` boolean NOT NULL DEFAULT false,
            PRIMARY KEY (`id`)
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
        ```

    2. Announcements:

        ```sql
        CREATE TABLE IF NOT EXISTS `announcements` (
            `id` int(11) NOT NULL AUTO_INCREMENT,
            `user_id` int(11) NOT NULL,
            `title` varchar(255) NOT NULL,
            `description` text NOT NULL,
            `photo` varchar(255) NOT NULL,
            `price` float NOT NULL,
            `is_offer` boolean NOT NULL,
            `created_at` timestamp NULL DEFAULT NULL,
            `updated_at` timestamp NULL DEFAULT NULL,
            PRIMARY KEY (`id`),
            FOREIGN KEY (`user_id`) REFERENCES `users` (`id`) ON DELETE CASCADE ON UPDATE CASCADE
        ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
        ```

4. Adding data:

    1. Users

        ```sql
        INSERT INTO `users` (`id`, `first_name`, `last_name`, `email`, `password`, `is_admin`) VALUES
        (1, 'John', 'Doe', 'john@doe.com', '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', true),
        (2, 'Jane', 'Doe', 'jane@doe.com', '$2y$10$TKh8H1.PfQx37YgCzwiKb.KjNyWgaHb9cbcoQgdIVFlYg7B77UdFm', false);
        ```

    2. Announcements

        ```sql
        INSERT INTO `announcements` (`user_id`, `title`, `description`, `photo`, `price`, `is_offer`) VALUES
        (1, 'Clean Code by Robert C. Martin', 'Clean Code is a book written by Robert C. Martin. It is considered to be one of the most influential books on software design. It is widely considered to be the best book on software design. It is also the first book to be written in English. It is a book about software design and its principles, and how to write good software.', 'https://images-na.ssl-images-amazon.com/images/I/51-QQQQQQQL._SX331_BO1,204,203,200_.jpg', 10.99, false),
        (2, "The Lord of the Rings by J.R.R. Tolkien', 'The Lord of the Rings is a fantasy novel written by English author and scholar J. R. R. Tolkien. The story began as a sequel to Tolkien's 1937 fantasy novel The Hobbit, but eventually developed into a much larger work. Written in stages between 1937 and 1949, The Lord of the Rings is one of the best-selling novels ever written, with over 150 million copies sold", 'https://images-na.ssl-images-amazon.com/images/I/51-QQQQQQQL._SX331_BO1,204,203,200_.jpg', 15.99, true);
        ```
