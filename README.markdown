# Overview #

This is a complete nginx configuration for (Drupal)[http://drupal.org] sites. It supports boost, images server and multiple sites. Configuration of generic components is encapsulated, so you only need to define the required stuff, like domain name, web root directory etc.

This is a complete nginx configuration that is meant to serve as a basis for your setup.

# Features #

* Drupal with clean URL's (of course!)
* Multisite - to add a site, just create a short config file and reload
* Multiple environments - like staging, development and production are possible (see example config file)
* Images server for static files and imagecache manipulation (You would want to override theme_imagecache for this).
* [Boost](http://drupal.org/project/boost) supported - if boost files exist they are used (Boost 5.x files scheme)
* Gzipped static files are served if they exist (see [javascript aggregator module](http://drupal.org/project/javascript_aggregator).
* Only allows to run the required PHP files (index.php, cron.php). The rest require a htpasswd. This provides a level of protection that is missing from most Drupal installations.
* Large fastcgi timeout - to allow long opeartions to run on PHP, until PHP times out.
* Use http://localhost/nginx_status to monitor server health, with tools like munin.

# Intallation #

* Clone this project, and point nginx conf file to nginx.conf (usually by editing  /etc/init.d/nginx, but that depends on your distribution).
* Make sure you have a fastcgi server (php-cgi mostly) running and listening on port 3000 (or change the port in conf/fastcgi)
* copy the file conf/example.conf to conf/yoursite.conf (must keep the .conf suffix) and edit to your needs.
* Modify the files conf/production, conf/staging and conf/dev to point to the directory of each env.

## Adding another site ##

Copy conf/example.conf and edit it to match the new site settings

# Troubleshooting

If you get an error about gzip_static line, either comment it out (and lose the automatic .gz files match) or recompile nginx with the '--with-http_gzip_static_module' configuration option.

If you get an error about stub_status module missing, comment those lines out, or recompile nginx with '--with-http_stub_status_module' configuration option.

If you want logs file not to be in the same directory as in the configuration file, create a symlink to the logs directory, something like:
# ln -s /var/logs/nginx conf/logs

# Contribution

  Fork this project on GitHub and send pull requests.

# Bugs, Features, Issues

  File a report on the issue tracker:
  [http://github.com/yhager/nginx_drupal/issues/](http://github.com/yhager/nginx_drupal/issues/)

# Questions

  Send me an e-mail (see LICENSE for my address).
