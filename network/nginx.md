# NGINX

## key points

- most oftenly used blocks: `server` and `location`. `location` can be nested.
- `location` can have settings like `proxy_pass`, `proxy_set_header`, &etc to reverse proxy. Noteworthy: nested `location` inherit from parent `location`. However, if `break` applies the inheritance will be ignored. In order to keep parent `location` rules applied, `last` is better used than `break`.
- `if` statement [is evil](https://www.nginx.com/resources/wiki/start/topics/depth/ifisevil/).
- nginx uses PCRE(Perl Compatible Regular Expression)