<img width="1536" height="1024" alt="t" src="https://github.com/user-attachments/assets/1e6395c2-e615-4524-8488-4e65887c22fe" />
# 🔍 Hafourenai Web Vulnerability Scanner

![Python](https://img.shields.io/badge/python-3.8+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Status](https://img.shields.io/badge/status-active-success.svg)
![Accuracy](https://img.shields.io/badge/accuracy-70--75%25-yellow.svg)

Professional-grade web vulnerability scanner dengan **ML-style behavioral analysis**, **context-aware detection**, dan **advanced anti-ban protection**.

---

## ✨ Features

### **Core Vulnerability Detection**
- 🎯 **SQL Injection** - Error, Union, Time-based, Boolean-based dengan multi-technique verification
- 🎯 **XSS (Cross-Site Scripting)** - Reflected, DOM-based dengan context analysis
- 🎯 **LFI (Local File Inclusion)** - Multi-file verification dengan pattern matching
- 🎯 **SSRF (Server-Side Request Forgery)** - Internal endpoint discovery
- 🎯 **CSRF** - Token validation dan form analysis
- 🎯 **Security Headers** - Missing X-Frame-Options, CSP, HSTS analysis
- 🎯 **Sensitive Data Exposure** - Credentials, API keys, config files
- 🎯 **Authentication Bypass** - Header manipulation testing

### **Advanced Detection Engine**
- 🧠 **Behavioral Analysis** - ML-style differential response analysis
- 🎯 **Context-Aware Detection** - Injection point analysis (script/attribute/tag)
- ✅ **Multi-Technique Verification** - Minimum 2 confirmations per finding
- 📊 **Confidence Scoring** - 0-100% confidence rating
- 🔄 **Smart Crawling** - Deep URL discovery dengan JavaScript, sitemap, API analysis
- 📈 **Professional HTML Reports** - Beautiful visualization dengan statistics

### **Anti-Ban Protection** 🛡️
- 🔄 **Proxy Rotation** - Automatic IP rotation dari proxy list
- 🧅 **TOR Integration** - Route traffic through TOR network
- ⏱️ **Adaptive Rate Limiting** - Auto-adjust speed when blocked (exponential backoff)
- 🚨 **Block Detection** - Real-time detection (403, 429, 503, captcha, cloudflare)
- 🔁 **Auto-Retry System** - 3x retry dengan proxy switching
- ❄️ **Cooldown Mechanism** - 30s-300s delay when rate-limited
- 📊 **Proxy Health Monitoring** - Track success rates per proxy

---

## 🚀 Quick Start

### **Installation**
```bash
# Clone repository
git clone https://github.com/hafourenai/hafourenai-webscan-just4me.git


# Install dependencies
pip install -r requirements.txt
```

### **Basic Usage**
```bash
# Simple scan
python honey.py http://target.com

# Stealth mode (slower, safer)
python honey.py http://target.com --stealth

# With proxies (recommended)
python honey.py http://target.com --proxy-file proxies.txt

# Maximum protection (TOR + Proxies + Stealth)
python honey.py http://target.com \
  --proxy-file proxies.txt \
  --use-tor \
  --stealth \
  --rate 0.3
```

---

## 📖 Complete Usage Guide

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

### **Usage Examples**

#### **1. Basic Vulnerability Scan**
```bash
# For learning/testing
python honey.py https://testphp.vulnweb.com
```

#### **2. Stealth Scan (Production Sites)**
```bash
python honey.py http://target.com \
  --stealth \
  --depth 7 \
  --threads 10 \
  --rate 0.5
```

#### **3. Scan with Proxy Protection**
```bash
# Setup proxies
echo "user:pass@proxy1.com:8080" > proxies.txt
echo "user:pass@proxy2.com:3128" >> proxies.txt

# Scan with rotating IPs
python honey.py http://target.com \
  --proxy-file proxies.txt \
  --stealth \
  --rate 0.5
```

#### **4. Maximum Anonymity (TOR + Proxies)**
```bash
# Start TOR
sudo service tor start

# Scan through TOR + Proxies
python honey.py http://target.com \
  --proxy-file proxies.txt \
  --use-tor \
  --stealth \
  --rate 0.2 \
  -d 5
```

#### **5. Aggressive Bug Bounty Scan**
```bash
python honey.py http://target.com \
  --aggressive \
  --threads 20 \
  --depth 10 \
  --rate 2.0
```

#### **6. High-Value Target (Cloudflare/WAF)**
```bash
python honey.py http://target.com \
  --proxy-file proxies.txt \
  --use-tor \
  --stealth \
  --rate 0.1 \
  --threads 3 \
  -d 3
```

---

## 🎓 Proxy Setup Guide

### **Option 1: Webshare.io (FREE - Recommended)** ⭐

**Best for beginners - 10 free proxies forever!**

1. **Sign up**: https://www.webshare.io/
2. **Download proxies**: Dashboard → Proxy → List → Download
   - Format: `IP:Port:Username:Password`
3. **Convert format**:
```bash
# Create converter
cat > convert_proxies.py << 'EOF'
input_file = 'webshare_proxies.txt'
output_file = 'proxies.txt'

with open(input_file, 'r') as f:
    lines = f.readlines()

with open(output_file, 'w') as f:
    for line in lines:
        parts = line.strip().split(':')
        if len(parts) == 4:
            ip, port, user, pwd = parts
            f.write(f"{user}:{pwd}@{ip}:{port}\n")

print("✓ Converted! Check proxies.txt")
EOF
```

4. **Use with scanner**:
```bash
python honey.py http://target.com --proxy-file proxies.txt
```

### **Option 2: Free Proxy Scraper** 💰

**Free but lower quality (20-30% success rate)**
```bash
# Use with scanner
python honey.py http://target.com --proxy-file proxies.txt
```

### **Option 3: Premium Proxies** 💎

For professional penetration testing:

| Service | Price | Quality | Best For |
|---------|-------|---------|----------|
| [Webshare.io](https://webshare.io) | FREE (10) / $2.95 | ⭐⭐⭐⭐ | Learning |
| [Smartproxy](https://smartproxy.com) | $75/5GB | ⭐⭐⭐⭐⭐ | Professional |
| [Bright Data](https://brightdata.com) | $500/40GB | ⭐⭐⭐⭐⭐ | Enterprise |

---

## 🔧 Configuration

### **Proxy File Format**
```txt
# proxies.txt
username:password@ip:port
user1:pass1@123.45.67.89:8080
user2:pass2@98.76.54.32:3128

# OR simple format (no auth)
1.2.3.4:8080
5.6.7.8:3128
```

### **Rate Limiting Recommendations**

| Target Type | Rate | Mode | Threads | Use Case |
|-------------|------|------|---------|----------|
| **Localhost/Lab** | 5.0 | Normal | 20 | Testing/Development |
| **Small Sites** | 2.0 | Normal | 15 | Basic websites |
| **Medium Sites** | 1.0 | Stealth | 10 | Corporate sites |
| **Large Sites** | 0.5 | Stealth | 10 | E-commerce, News |
| **WAF Protected** | 0.3 | Stealth + Proxies | 5 | Cloudflare, Akamai |
| **High Security** | 0.1 | Stealth + TOR | 3 | Banks, Government |

---

## 📊 Performance & Accuracy

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

### **Benchmark Tests**
```bash
# Test Site: testphp.vulnweb.com
# Mode: Normal (rate=1.0, depth=5)
# Results:
# - Duration: 3m 45s
# - URLs Scanned: 67
# - Vulnerabilities Found: 12 (8 High, 3 Medium, 1 Low)
# - Accuracy: 75% (9/12 confirmed exploitable)
```

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

---

## 🛡️ Legal Disclaimer

⚠️ **IMPORTANT: READ BEFORE USE**

This tool is for **AUTHORIZED SECURITY TESTING ONLY**.

### **✅ Legal Use**
- Testing your own websites/applications
- Authorized penetration testing with **written permission**
- Bug bounty programs (**within program scope**)
- Educational/research in isolated lab environments
- Security assessments with client approval

### **❌ Illegal Use**
- Scanning websites **without authorization**
- Exploiting vulnerabilities on third-party systems
- Denial of service attempts
- Any malicious activities
- Unauthorized access attempts

### **⚖️ Legal Consequences**
Unauthorized scanning may violate:
- Computer Fraud and Abuse Act (CFAA) - USA
- Computer Misuse Act - UK
- Cybercrime laws in your jurisdiction

**Penalties:** Fines, imprisonment, civil liability

**THE AUTHORS ARE NOT RESPONSIBLE FOR MISUSE OF THIS TOOL.**

---

## 🏆 Comparison with Other Tools

### **vs Nikto/Dirb/DirBuster**
✅ Context-aware detection (not just pattern matching)  
✅ Multi-technique verification  
✅ Confidence scoring  
✅ Beautiful HTML reports  
✅ Built-in anti-ban  
❌ Less specialized for directory bruteforce  

### **vs Burp Suite Community**
✅ Fully automated  
✅ Proxy rotation built-in  
✅ Free & open source  
✅ Behavioral analysis  
❌ No manual testing tools  
❌ Less comprehensive than Burp Pro  

### **vs OWASP ZAP**
✅ Lighter & faster startup  
✅ Better proxy management  
✅ Simpler configuration  
✅ Advanced anti-ban features  
❌ Fewer total features  
❌ No GUI  

### **vs sqlmap/XSStrike**
✅ All-in-one scanner  
✅ Automatic crawling  
✅ Multiple vulnerability types  
❌ Less specialized per vulnerability  
❌ Fewer exploitation options  

### **vs Acunetix/Netsparker (Commercial)**
✅ Free & open source  
✅ Customizable  
✅ Good for learning  
❌ No browser automation  
❌ Lower accuracy (~70% vs ~90%)  
❌ No compliance reporting  

---

## 📈 Roadmap

### **v3.0 (Planned)**
- [ ] Browser automation (Selenium/Playwright) for XSS verification
- [ ] GraphQL/WebSocket advanced testing
- [ ] Machine learning model for WAF bypass
- [ ] Mobile app API testing support
- [ ] Advanced CAPTCHA detection & bypass suggestions
- [ ] Distributed scanning (multiple nodes)

### **v2.1 (Current)**
- [x] ML-style behavioral analysis
- [x] Context-aware detection
- [x] Multi-technique verification
- [x] Anti-ban protection
- [x] TOR integration
- [x] Confidence scoring

---
## 📧 Contact & Support

- **Author**: Hafourenai
- **GitHub**: [@hafourenai](https://github.com/hafourenai)
- **Email**: hafourenai@gmail.com

### **Support the Project**
- ⭐ Star this repository
- 🐛 Report bugs
- 💡 Suggest features
- 🔀 Contribute code
- ☕ Buy me a coffee

## 📄 License

MIT License - see [LICENSE](LICENSE) file for details.

### **MIT License Summary**
- ✅ Commercial use
- ✅ Modification
- ✅ Distribution
- ✅ Private use
- ⚠️ No liability
- ⚠️ No warranty

---
### **Development Setup**
```bash
# Clone
git clone https://github.com/hafourenai/hafourenai-webscan-just4me.git


# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dev dependencies
pip install -r requirements.txt
pip install pytest black flake8

# Run tests
pytest tests/

# Format code
black honey.py

# Lint
flake8 honey.py --max-line-length=120
```

---

## 📚 Resources

### **Learning Materials**
- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
- [HackerOne Hacker101](https://www.hacker101.com/)
- [PentesterLab](https://pentesterlab.com/)

### **Practice Targets**
- [DVWA](http://www.dvwa.co.uk/) - Damn Vulnerable Web App
- [bWAPP](http://www.itsecgames.com/) - Buggy Web Application
- [WebGoat](https://owa
