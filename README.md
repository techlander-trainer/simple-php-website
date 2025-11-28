# Simple PHP-based website

This project is used in the GitHub documentation to guide users through the process of converting a project written on one language to another language - for example, from PHP to Python.

The repository is derived from the public GitHub repository [banago/simple-php-website](https://github.com/banago/simple-php-website).

## Installation

To generate the website output from this project:

1. Clone the project to your local computer.
1. Install PHP on your computer.
1. In a terminal, navigate to the project folder.
1. Run `php -S localhost:8080`.
1. In a web browser, go to http://localhost:8080.

## HTTPS Configuration

### Using Apache with mod_ssl

To enable HTTPS with Apache:

1. Ensure `mod_ssl` and `mod_rewrite` are enabled.
1. Configure your virtual host with SSL certificates.
1. Edit `.htaccess` and uncomment the HTTPS redirect rules:
   ```apache
   RewriteCond %{HTTPS} off
   RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
   ```

### Using PHP Built-in Server with HTTPS

For local development with HTTPS:

1. Generate a self-signed SSL certificate:
   ```bash
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
     -keyout localhost.key -out localhost.crt \
     -subj "/CN=localhost"
   ```

1. Use a PHP wrapper or reverse proxy (e.g., nginx, Caddy) to handle SSL termination.

### Enabling HTTPS Redirect in PHP

To enforce HTTPS redirects in the application, call the `https_redirect()` function in `index.php`:

```php
require 'includes/config.php';
require 'includes/functions.php';

https_redirect(true); // Enable HTTPS redirect

init();
```

The function handles:
- Standard HTTPS detection via `$_SERVER['HTTPS']`
- Proxy/load balancer detection via `X-Forwarded-Proto` header
- Port-based detection (port 443)

## License

MIT
