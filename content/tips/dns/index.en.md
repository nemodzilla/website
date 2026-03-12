---
title: "DNS — Understanding all record types"
description: "Explanation of DNS records: A, AAAA, MX, TXT, CNAME, DNSSEC, CAA, SPF, DMARC, Google Analytics and Tag Manager"
date: 2026-03-12
slug: "dns-explained"
categories:
    - Tips
tags:
    - dns
    - network
draft: false
---

## What is DNS?

DNS (Domain Name System) is the Internet's phonebook. It maps human-readable domain names (`nemodzilla.xyz`) to machine IP addresses (`185.199.108.153`). Without DNS, you'd need to memorize IPs for every website.

---

## Basic records

### A — IPv4
Points a domain to an **IPv4** address (4 octets).
```
nemodzilla.xyz  →  185.199.108.153
```

Most common record type. You have several for your site (GitHub Pages redundancy).

### AAAA — IPv6
Same but for an **IPv6** address (128-bit, format `2001:db8::1`).
```
nemodzilla.xyz  →  2606:50c0:8000::153
```

IPv6 is IPv4's successor, needed because IPv4 addresses are exhausted.

### CNAME — Alias
Points a domain to **another domain name** (not an IP directly).
```
www.nemodzilla.xyz  →  nemodzilla.github.io
```

> ⚠️ A CNAME cannot coexist with other records on the same name. That's why the root (`@`) uses A records and `www` uses a CNAME.

### MX — Mail Exchange
Tells which server handles **emails** for your domain.
```
nemodzilla.xyz  →  mail.protonmail.ch  (priority 10)
```

Priority (number) determines attempt order — lower number = higher priority.

### TXT — Free text
Free text record, used for **domain verification** and email policies (SPF, DMARC).
```
nemodzilla.xyz  →  "v=spf1 include:_spf.google.com ~all"
```

---

## Email security

### SPF — Sender Policy Framework
A **TXT** record listing servers authorized to send emails on your behalf.
```
v=spf1 include:_spf.google.com ~all
```

- `include:` → authorized servers
- `~all` → others are suspicious (soft fail)
- `-all` → others are rejected (hard fail)

Without SPF, anyone can send an email pretending to be `@nemodzilla.xyz`.

### DMARC — Domain-based Message Authentication
Policy telling receiving servers what to do if SPF/DKIM fail.
```
v=DMARC1; p=reject; rua=mailto:dmarc@nemodzilla.xyz
```

- `p=none` → monitor only
- `p=quarantine` → send to spam
- `p=reject` → reject the email

### DKIM — DomainKeys Identified Mail
Cryptographic signature added to emails to prove they came from you. Configured server-side, published as TXT in DNS.

---

## DNS Security

### DNSSEC
Adds **cryptographic signatures** to DNS records to prevent cache poisoning (an attacker redirecting your domain to a fake IP).

Cloudflare can enable it in one click: **DNS** → **DNSSEC** → Enable.

### CAA — Certification Authority Authorization
Defines which **certificate authorities** are allowed to issue SSL certificates for your domain.
```
nemodzilla.xyz  CAA  0 issue "letsencrypt.org"
```

Prevents a rogue CA from issuing a certificate for your domain without your knowledge.

---

## Google Analytics & Tag Manager

### Google Analytics (GA4)
**Audience measurement** tool — tells you how many visitors you have, where they come from, which pages they visit, how long they stay.

ID looks like: `G-XXXXXXXXXX`

To enable on Hugo Theme Stack, add to `params.toml`:
```toml
[analytics.google]
    id = "G-XXXXXXXXXX"
```

### Google Tag Manager (GTM)
A **script container** that lets you add/modify tracking scripts (Analytics, ad pixels, etc.) without touching the site's code.

ID looks like: `GTM-XXXXXXX`

Difference from Analytics:
- **Analytics** → collects and analyzes data
- **Tag Manager** → manages *how* scripts are injected into the page

For a personal site, Google Analytics alone is more than enough. Tag Manager is useful when multiple tracking tools coexist and you want to manage them without redeploying.

---

## Summary

| Record | Role |
|--------|------|
| A | Domain → IPv4 |
| AAAA | Domain → IPv6 |
| CNAME | Domain → another domain |
| MX | Domain → mail server |
| TXT | Free text (SPF, DMARC, verification) |
| CAA | Authorized SSL authorities |
| DNSSEC | DNS cryptographic signatures |
| SPF | Authorized mail servers |
| DMARC | Email spoofing policy |