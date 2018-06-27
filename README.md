# Nginx config snippets collection
A selection of common use config blocks for Nginx web server. Tested against Nginx 1.10.0.

- [denygit.conf](#denygitconf)
- [denyhtaccess.conf](#denyhtaccessconf)
- [forwardslash.conf](#forwardslashconf)
- [frontcontroller.conf](#frontcontrollerconf)
- [multislashremove.conf](#multislashremoveconf)
- [phpfastcgi.conf](#phpfastcgiconf)
- [releasecssjs.conf](#releasecssjsconf)
- [releasecssjsexpires.conf](#releasecssjsexpiresconf)
- [removewww.conf](#removewwwconf)

## denygit.conf
[`denygit.conf`](conf/denygit.conf) location block to deny access to Git related files and directories. Will 404 any request made to a matching file/path pattern.

## denyhtaccess.conf
[`denyhtaccess.conf`](conf/denyhtaccess.conf) location block to 404 error any requests matching an Apache web server `.htaccess` directory level configuration file.

## forwardslash.conf
[`forwardslash.conf`](conf/forwardslash.conf) is an `if` condition for use inside a location block to ensure all requested URL paths end with a trailing forward slash, with a 301 redirect otherwise.

## frontcontroller.conf
[`frontcontroller.conf`](conf/frontcontroller.conf) offers an example of a internal rewrite rule to route all requests not considered a file (e.g. a fullstop followed by 2-4 characters `[a-z0-9]`) to an `index.php` script in the document root.

## multislashremove.conf
[`multislashremove.conf`](conf/multislashremove.conf) is an `if` condition for use inside a location block to redirect URL paths containing multiple sequences of forward slashes, with a 301 redirect.

## phpfastcgi.conf
[`phpfastcgi.conf`](conf/phpfastcgi.conf) passes PHP script requests to a FastCGI backend - such as [PHP-FPM](http://php.net/manual/en/install.fpm.php). Works in tandem with [`phpfastcgiparam.conf`](conf/phpfastcgiparam.conf), which defines Nginx FastCGI settings.

## releasecssjs.conf
[`releasecssjs.conf`](conf/releasecssjs.conf) rewrite rule for 'cache busting' requests to CSS/JavaScript resources back to their canonical source.

The 16 digit hash examples (below) could be either:
- Randomly generated upon deploy.
- Derived from Git SHA1 release.

For example:
```
Request: /57cb6492897bd7b7/css/style.css
Rewrite: /css/style.css

Request: /897bd7b71310c7a9/js/app.js
Rewrite: /js/app.js
```

## releasecssjsexpires.conf
[`releasecssjsexpires.conf`](conf/releasecssjsexpires.conf) is an extension to [`releasecssjs.conf`](#releasecssjsconf), written as a location block with a 30 day `Expires` / `Cache-Control: max-age=SECONDS` window for the requested file.

## removewww.conf
[`removewww.conf`](conf/removewww.conf) is a template for the recommended Nginx way of handling redirects in the style of `http://www.domain.com/URI_PATH` to `http://domain.com/URI_PATH`.
