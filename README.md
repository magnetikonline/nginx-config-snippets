# Nginx config snippets collection
A selection of common use config blocks for Nginx web server. Tested against Nginx 1.6.1.

- [denygit.conf](#denygitconf)
- [denyhtaccess.conf](#denyhtaccessconf)
- [forwardslash.conf](#forwardslashconf)
- [multislashremove.conf](#multislashremoveconf)
- [releasecssjs.conf](#releasecssjsconf)
- [releasecssjsexpires.conf](#releasecssjsexpiresconf)
- [removewww.conf](#removewwwconf)

## denygit.conf
Location block to deny access to Git related files and directories. Will 404 any request made to a matching file/path pattern.

## denyhtaccess.conf
Location block to 404 error any requests matching an Apache web server `.htaccess` directory level configuration file.

## forwardslash.conf
If condition used inside a location block to ensure all requested URL paths end with a trailing forward slash. Will 301 redirect all path requests without a trailing slash.

## multislashremove.conf
If condition used inside a location block to redirect all URL paths with multiple sequences of forward slashes, with a 301 redirect.

## releasecssjs.conf
Rewrite rule for 'cache busting' requests to CSS/JavaScript documents back to their root/source document. The 16 digit hash might be randomly generated on app deploy, or even better taken from the Git SHA1 app release/tag.

For example:
```
Request: /57cb6492897bd7b7/css/style.css
Rewrite: /css/style.css

Request: /897bd7b71310c7a9/js/app.js
Rewrite: /js/app.js
```

## releasecssjsexpires.conf
Same as `releasecssjs.conf` above, but written as a location block with a 30 day expires window for the requested file.

## removewww.conf
A template for the recommeded Nginx way of handling redirects of `http://www.domain.com` to `http://domain.com`.
