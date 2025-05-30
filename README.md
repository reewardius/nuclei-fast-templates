# nuclei-fast-templates

**Passive Fuzzing**
```bash
katana -u root.txt -ps -f qurl -o passive.txt && \
uro -i passive.txt -o dedupe.txt && \
nuclei -l dedupe.txt -tags fuzzing-req -dast -t nuclei-fast-templates/ -fuzz-param-frequency 10000
```
**Active Fuzzing**
```bash
katana -u alive_http_services.txt -ct 3m -ef js,png,css,jpeg,jpg,woff2 -c 50 -p 50 -rl 300 -d 5 -iqp -o katana.txt && \
nuclei -l katana.txt -tags fuzzing-req -dast -t nuclei-fast-templates/ -fuzz-param-frequency 10000
```

If you want to scan for a specific vulnerability, replace **-tags fuzzing-req** with a tag from the list below.

| Tag               | Description                                      |
|------------------|------------------------------------------------|
| `fuzzing-req`   | General fuzzing for all vulnerabilities         |
| `fuzzing-rce`   | Fuzzing for Remote Code Execution (RCE)         |
| `fuzzing-redirect` | Fuzzing for open redirects                    |
| `fuzzing-xxe`   | Fuzzing for XML External Entity (XXE) injection |
| `fuzzing-lfi`   | Fuzzing for Local File Inclusion (LFI)          |
| `fuzzing-xss`   | Fuzzing for Cross-Site Scripting (XSS)          |
| `fuzzing-ssrf`  | Fuzzing for Server-Side Request Forgery (SSRF)  |
| `fuzzing-ssti`  | Fuzzing for Server-Side Template Injection (SSTI) |
| `fuzzing-sqli`  | Fuzzing for SQL Injection (SQLi)                |

**Active Scan**
```bash
subfinder -dL root.txt -all -silent -o subs.txt && \
naabu -l subs.txt -s s -tp 100 -ec -c 50 -o naabu.txt && \
httpx -l naabu.txt -rl 500 -t 200 -o alive_http_services.txt && \
nuclei -l alive_http_services.txt -etags fuzzing-req,cache,logs,backup,listing -t nuclei-fast-templates/ -rl 1000 -c 100
```

**Web Cache Poisoning Templates**

It is better to run cache, logs and backup templates separately, as they significantly increase the scan time.
```bash
nuclei -l resolved -tags cache -t nuclei-fast-templates/
```

**Backup Templates**
```bash
nuclei -l resolved -tags backup -t nuclei-fast-templates/
```

**Logs Templates**
```bash
nuclei -l resolved -tags logs -t nuclei-fast-templates/
```

**Listing Templates**
```bash
nuclei -l resolved -tags listing -t nuclei-fast-templates/
```
