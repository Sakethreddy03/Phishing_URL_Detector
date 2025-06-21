# Phishing URL Checker

This project is a simple **JavaScript-based Phishing URL Detection Tool** that helps identify suspicious or potentially harmful URLs. It uses a set of heuristic rules to detect phishing attempts based on the structure and content of the URL.

## Live Demo

Paste a URL into the input box and click **"Check URL"**. The tool will analyze the URL and display whether it appears to be safe or suspicious.

---

## Features

- Detects:
  - IP address-based URLs
  - URLs with `@` symbols (common in phishing)
  - Very long URLs
  - Excessively nested paths
  - Hyphenated domains
  - Known URL shorteners
  - Suspicious keywords (e.g., `login`, `bank`, `verify`)
  - Dangerous file extensions (e.g., `.exe`, `.zip`)
  - Double slashes in paths
  - Odd `www-` subdomains
  - Highly nested domain names
  - Random long subdirectories

---

## Detection Logic

The detection is handled by the `isSuspiciousURL(url)` function using the following rules:

```javascript
if (/^\d{1,3}(\.\d{1,3}){3}$/.test(domain)) return true; // IP address
if (url.includes('@')) return true;                      // @ symbol
if (url.length > 75) return true;                        // Long URL
if (url.split('/').length > 8) return true;              // Too many slashes
if (domain.includes('-')) return true;                   // Hyphen in domain
if (shorteners.some(short => domain.includes(short))) return true; // Known shorteners
if (suspiciousWords.some(word => url.includes(word))) return true; // Suspicious keywords
if (suspiciousExtensions.some(ext => url.endsWith(ext))) return true; // Dangerous files
if (pathname.includes("//")) return true;                // Double slashes in path
if (domain.startsWith("www-")) return true;              // Weird subdomain
if (domain.split('.').length > 4) return true;           // Very nested domains
if (pathname.match(/(\/\w{10,})/)) return true;          // Long random folder names
