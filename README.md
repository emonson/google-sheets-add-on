This repo houses the code used in the google sheets "Send to Elasticsearch" add-on.

See the [Wiki](https://github.com/elastic/google-sheets-add-on/wiki/Configuration-Help) for help configuring this.

My own modifications are targeted toward getting this add-on to work with the
AWS ES (Elasticsearch), which right now is ES v5.1.

Main problem with the original script seems to be that AWS ES has default setting of

```
rest.action.multi.allow_explicit_index: false
```

and the script is written to use a root URL (i.e. not including index and type in the URL path)
but specify and index and index_type in the data posted to ES. This caused ES to return
an error of `explicit index in bulk is not allowed`. So, I changed the bulk data format
and URL to accomodate this.