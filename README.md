# nuclei-fast-templates

**Passive Fuzzing**
```
katana -u root.txt -ps -o passive.txt
uro -i passive.txt -o dedupe.txt 
nuclei -l dedupe.txt -tags fuzzing-rce,fuzzing-redirect,fuzzing-xxe,fuzzing-lfi,fuzzing-xss,fuzzing-ssrf,fuzzing-ssti
```

**Active Scan**
```
subfinder -dL root.txt -all -silent -o subdomains.txt
dnsx -l subdomains -silent -o resolved
nuclei -l resolved -etags fuzzing-rce,fuzzing-redirect,fuzzing-xxe,fuzzing-lfi,fuzzing-xss,fuzzing-ssrf,fuzzing-ssti
```