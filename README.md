#### Nuclei AI Templates Scanning
```bash
subfinder -dL root.txt -all -silent -o subs.txt && \
naabu -l subs.txt -s s -tp 100 -ec -c 50 -o naabu.txt && \
httpx -l naabu.txt -rl 500 -t 200 -o alive_http_services.txt && \
nuclei -l alive_http_services.txt -t nuclei-ai-templates/ -rl 1000 -c 100
```
#### Nuclei Active DAST Scanning with AI Templates
```bash
katana -u alive_http_services.txt -ct 3m -ef js,png,css,jpeg,jpg,woff2 -c 50 -p 50 -rl 300 -d 5 -iqp -o katana.txt && \
nuclei -l katana.txt -t nuclei-ai-templates/ -dast -fuzz-param-frequency 10000
```
#### Possible Social Link Hijacking
```bash
nuclei -l alive_http_services.txt -t nuclei-ai-templates/others/broken-link-hijacking.yaml -o results.txt -headless && \
awk -F'\\["|\"]' '{if (NF>1) print $2}' results.txt | tr ',' '\n' | sed 's/"//g' | sort -u > social_links.txt && \
httpx -l social_links.txt -mc 404
```
