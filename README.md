# chart-pysocha-site

If you have a pysocha static site (or any static site you can shove in a single directory) this chart is there to give you a helm way to deploy it to kubernetes. Ridiculously simple.


## Deploy one

```
helm repo add catalyst-helm https://raw.githubusercontent.com/catalystcommunity/charts/main
helm repo update
helm upgrade --install --create-namespace --namespace mypysochanamespace mypysochasite -f YOURVALUES.yaml catalyst-helm/pysocha-site
```

This will create a namespace and a release (replace mypysochasite with your release name) and setup a basic single pod with a service based on the domain name. You will need a values file with at a minimum:

`domain`: your "domain.tld" which will default to "notreal.com" so you must change these, really
`image.repository`: your image repo, without the tag
`image.tag`: the tag, can be latest if you wish, but we encourage you not to. We believe in your ability to manage versions.

Some optional changes like your site path and whatnot are available in the default value.yaml file

This will redirect any www.`domain.tld` to `domain.tld` on https as well. If you want to use www for some reason, uh, PR something that defaults to non-www and allows an override. If it's good we'll consider it. 

Keep in mind that this does not manage any TLS, despite using Caddy. TLS should be handled by your ingress or your own mTLS sidecars. Caddy wasn't really built for kubernetes in thei automatic https bits. If that changes, we might update, or we might switch to simply using another http server, who knows.

## Contributions

Talk to us on discord (link kept most up to date in our community profile: https://github.com/catalystcommunity ), BEFORE you do anything. We're picky about what our projects do. They our happy places to work in.