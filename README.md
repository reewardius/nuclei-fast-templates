# nuclei-fast-templates

**Passive Fuzzing**
```
katana -u root.txt -ps -o passive.txt
uro -i passive.txt -o dedupe.txt
nuclei -l dedupe.txt -tags fuzzing-req
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
```
subfinder -dL root.txt -all -silent -o subdomains.txt
dnsx -l subdomains -silent -o resolved
nuclei -l resolved -etags fuzzing-req,cache,logs,backup,listing
```

**Web Cache Poisoning Templates**

It is better to run cache, logs and backup templates separately, as they significantly increase the scan time.
```
nuclei -l resolved -tags cache
```

**Backup Templates**
```
nuclei -l resolved -tags backup
```

**Logs Templates**
```
nuclei -l resolved -tags logs
```

**Listing Templates**
```
nuclei -l resolved -tags listing
```
