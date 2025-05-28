#### Nuclei AI Templates Scanning
```
nuclei -l targets.com -t nuclei-ai-templates/
```
#### Nuclei DAST Scanning with AI Templates
```
katana -u http://testphp.vulnweb.com -o katana.txt && nuclei -l katana.txt -t nuclei-ai-templates/ -dast -fuzz-param-frequency 10000
```
