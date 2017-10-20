
An app to redirect a `www.example.com` to `example.com`.

## Disclaimer

It is a hack.

It is intended to be so.

Yes, I know about [from-to-www-redirect](https://github.com/kubernetes/ingress-nginx/blob/master/docs/user-guide/annotations.md#redirect-from-to-www) in Nginx ingress controller.

## Why then?!

I made it for the case when there is no possibility to use Nginx ingress controller's embedded functionality.

E.g., in our case:

We have different certificates for `www`-domain & `non-www`-domain. That just doesn't work on a vanilla Nginx ingress controller. And writing a hack for the latter results into a too complex configuration.

## How to install

I cannot force you to clone this chart multiple times, put your TLS crt/key files into its dir and run it only after that. I intend this chart to be used for multiple apps. Therefore it is hard to automate TLS secrets creation for you. Sorry. You'll have to do it yourself:

```shell
kubectl create secret TLS www.example.com-tls --key www.example.com.key --cert www.example.com.crt -n ebay-mag-2

# And so on...
```

Set the array of the domains you wish to have a redirect to in your `values.yaml`:

```yaml
domains:
  - example.com
  - example2.com
```

```shell
helm install -f values.yaml www-redirect-chart/
```