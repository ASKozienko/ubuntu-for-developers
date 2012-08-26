# Apache for Developers

### `fastcgi`
```bash
<IfModule mod_fastcgi.c>
  FastCgiIpcDir /var/lib/apache2/fastcgi

  Alias /php5-fcgi-username /usr/lib/cgi-bin/php5-fcgi-username
  FastCgiExternalServer /usr/lib/cgi-bin/php5-fcgi-username -idle-timeout 300 -socket /var/run/php5-fpm-username.sock -pass-header Authorization
</IfModule>
```