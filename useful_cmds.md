#Useful commands
These are all unsorted:

```bash
cat 20160420082525_http___jelna_hi2_ro_ss_txt | grep -Eo "(http|https)://[a-zA-Z0-9./?=_-]*" | sort | uniq >> URLs.txt

cat cowrie.log* | grep virustotal
```
