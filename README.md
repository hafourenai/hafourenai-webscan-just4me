<img width="1536" height="1024" alt="t" src="https://github.com/user-attachments/assets/4128ffd7-8179-4d19-bf54-255494ba075e" />

# Honey Web Vulnerability Scanner


### **Installation**
```bash
# Clone repository
git clone https://github.com/hafourenai/hafourenai-webscan-just4me.git
cd hafourenai-webscan-just4me

python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```


---

### **Command Line Options**
```
python honey.py <target> [options]

Required:
  target                Target URL (e.g., http://example.com)

Scanning Options:
  -t, --threads INT    Number of threads (default: 15)
  -d, --depth INT      Crawl depth (default: 5)
  --stealth           Stealth mode (2-5s delay, human-like patterns)
  --aggressive        Aggressive mode (faster, higher risk)

Anti-Ban Options:
  --proxy-file FILE   Path to proxy list file
  --use-tor           Use TOR network for anonymity
  --rate FLOAT        Requests per second (default: 1.0)
```

### **Usage**

#### **1. Basic Vulnerability Scan**
```bash
# For learning/testing
python honey.py https://testphp.vulnweb.com
```

#### **2. Stealth Scan (Production Sites)**
```bash
python honey.py http://target.com --stealth --depth 7 --threads 10 --rate 0.5
```

#### **3. Scan with Proxy Protection**
```bash
python honey.py http://target.com --proxy-file proxies.txt --stealth --rate 0.5
```
#### **4. Maximum Anonymity (TOR + Proxies)**
```bash
# Start TOR
sudo service tor start

python honey.py http://target.com --proxy-file proxies.txt --use-tor --stealth --rate 0.2 -d 5

# Stop TOR
sudo service tor stop
```

#### **5. Aggressive Bug Bounty Scan**
```bash
python honey.py http://target.com --aggressive --threads 20 --depth 10 --rate 2.0
```

#### **6. High-Value Target (Cloudflare/WAF)**
```bash
python honey.py http://target.com --proxy-file proxies.txt --use-tor --stealth --rate 0.1 --threads 3 -d 3
```

---

### **Detection Accuracy** (Realistic Estimates)

| Vulnerability Type | Accuracy | Method |
|-------------------|----------|---------|
| **SQL Injection** | ~75% | Multi-technique + behavioral analysis |
| **XSS** | ~70% | Context-aware + multi-vector |
| **LFI** | ~80% | Multi-file verification |
| **CSRF** | ~85% | Token analysis |
| **Security Headers** | ~95% | Direct header check |
| **Overall Average** | **~70-75%** | Verified findings only |

### **Performance Metrics**

- **Scan Speed**: 50-200 requests/minute (depends on rate limit)
- **Memory Usage**: 50-200 MB (depends on site size)
- **CPU Usage**: Low-Medium (multi-threaded, non-blocking I/O)
- **False Positive Rate**: ~15-20% (with verification enabled)
- **False Negative Rate**: ~25-30% (complex/obfuscated vulnerabilities may be missed)

---

## ⚠️ Limitations

### **Technical Limitations**
1. ❌ **No Browser Automation** - Cannot verify JavaScript XSS execution
2. ❌ **No CAPTCHA Bypass** - Will fail on sites with CAPTCHA
3. ❌ **Limited WAF Evasion** - Basic WAF bypass only (no ML-based evasion)
4. ❌ **No Blind XXE** - Only reflected XXE detection
5. ❌ **No WebSocket** - HTTP/HTTPS only
6. ❌ **No GraphQL Advanced** - Basic GraphQL endpoint discovery only
7. ⚠️ **Free Proxy Speed** - 2-10s per request (use premium for speed)

### **Detection Limitations**
- **Cannot detect:** Second-order SQLi, stored XSS (without revisit), blind SSRF
- **May miss:** Obfuscated payloads, custom WAF rules, rate-limited responses
- **False positives:** Uncommon in reflected vulnerabilities, but possible in stored/blind

### **Not Suitable For**
- ❌ Sites dengan CAPTCHA/reCAPTCHA aktif
- ❌ Heavy JavaScript single-page applications (SPAs)
- ❌ WebSocket/GraphQL complex mutations
- ❌ Mobile app API testing (tanpa custom configuration)
- ❌ Real-time applications (WebRTC, streaming)


