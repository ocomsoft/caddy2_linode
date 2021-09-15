# linode module for Caddy

This package contains a DNS provider module for [Caddy](https://github.com/caddyserver/caddy). It can be used to manage DNS records with linode accounts. In order to use this module, you must build caddy with [xcaddy](https://github.com/caddyserver/xcaddy).

```
xcaddy build --with github.com/ocomsoft/caddy2_linode
```


## Caddy module name

```
dns.providers.linode
```

## Config examples

To use this module for the ACME DNS challenge, [configure the ACME issuer in your Caddy JSON](https://caddyserver.com/docs/json/apps/tls/automation/policies/issuer/acme/) like so:

```json
{
  "module": "acme",
  "challenges": {
    "dns": {
      "provider": {
        "name": "linode",
        "api_key": "{env.LINODE_API_KEY}"
      }
    }
  }
}
```

or with the Caddyfile:

```
tls {
	dns linode {
        api_key {env.LINODE_API_KEY}
    }
}
```

You can replace `{env.LINODE_API_KEY}` with the actual auth token if you prefer to put it directly in your config instead of an environment variable.

A complete example

```
*.example.com {
    file_server
    tls {
        dns linode {
            api_key {env.LINODE_API_KEY}         
        }
    }
}
```
