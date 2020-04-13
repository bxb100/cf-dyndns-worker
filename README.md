# A dyndns provider in a CloudFlare worker

With me using CloudFlare and CloudFlare providing free workers, why would I bother with shady dyndns providers, it should be simple enough to implement myself.

This is what I came up with.

## Setup

You need wrangler to set this up.

You'll also need to create a few secrets (`wrangler secret put [-e prod] <NAME>`):

* `CF_TOKEN`: a token with edit permission on the zone's DNS (go to [your profile](https://dash.cloudflare.com/profile/api-tokens) and create a token with the `DNS:Edit` permission on your CF Zone)
* `CF_ZONE`: the CF zone id, as listed on the dashboard of the zone (scroll down, it's in the sidebar)
* `DOMAIN`: the record in the zone to set
* `PASSWORD`: the key to use to make sure people don't just update your DNS...

```bash
wrangler publish -e prod
```

Next up, you point your script to that URL using the following get parameters:

* `ipv4`: the new ipv4
* `ipv6`: the new ipv6
* `password`: the password you chose in the step above


## Notes

I recommend setting the `DOMAIN` secret to a random subdomain and then pointing a CloudFlare proxied CNAME to it. That way, it is harder to find out what your home IP is.
