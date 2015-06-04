This branch is the result you get when you finish day 2 of blogbee tutorial (except vendors and project configuration files).

The following installation instructions consider that you have already installed the application requirements such as git, composer, php and nginx or apache2, if not, see [blogbee tutorial day1](https://github.com/backbee/blogbee-docs/blob/master/doc/day1.md)

The result of the integration is available in integration folder.


How to install Day 2 results:

In your terminal
```
git clone https://github.com/backbee/blogbee.git && cd $_

git fetch origin day1:day1

git checkout day1

composer update

cd public

php -S localhost:8080
```

In your favorite navigator go to this page `localhost:8080/install.php`

Complete each form and follow the instructions.

Now you're ready to start Day 3.