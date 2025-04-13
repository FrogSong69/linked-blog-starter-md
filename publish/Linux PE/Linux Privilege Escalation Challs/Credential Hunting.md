
This is super easy 

Find the WordPress database password.

if we do a grep to find the wp-config.php file

find / -type f -name "wp-config.php" 2>/dev/null

we get it right away 

```
find / -type f -name "wp-config.php" 2>/dev/null
/var/www/html/wp-config.php
```

```
 cat /var/www/html/wp-config.php
<?php
/**
 * The base configuration for WordPress
...

/** MySQL database username */
define( 'DB_USER', 'wordpressuser' );

/** MySQL database password */
define( 'DB_PASSWORD', 'W0rdpr3ss_sekur1ty!' );
```