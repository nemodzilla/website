---
title: "DNS — Tout comprendre sur les enregistrements"
description: "Explication des enregistrements DNS : A, AAAA, MX, TXT, CNAME, DNSSEC, CAA, SPF, DMARC, Google Analytics et Tag Manager"
date: 2026-03-12
slug: "dns-explained"
categories:
    - Astuces
tags:
    - dns
    - réseau
draft: false
---

## C'est quoi le DNS ?

Le DNS (Domain Name System) est l'annuaire d'Internet. Il fait la correspondance entre un nom de domaine lisible (`nemodzilla.xyz`) et une adresse IP machine (`185.199.108.153`). Sans DNS, il faudrait retenir des IPs pour chaque site.

---

## Les enregistrements de base

### A — IPv4
Pointe un domaine vers une adresse **IPv4** (4 octets).
```
nemodzilla.xyz  →  185.199.108.153
```

C'est l'enregistrement le plus courant. Tu en as plusieurs pour ton site (redondance GitHub Pages).

### AAAA — IPv6
Même chose mais pour une adresse **IPv6** (128 bits, format `2001:db8::1`).
```
nemodzilla.xyz  →  2606:50c0:8000::153
```

IPv6 est le successeur d'IPv4, nécessaire car les adresses IPv4 sont épuisées.

### CNAME — Alias
Pointe un domaine vers **un autre nom de domaine** (pas une IP directement).
```
www.nemodzilla.xyz  →  nemodzilla.github.io
```

> ⚠️ Un CNAME ne peut pas coexister avec d'autres enregistrements sur le même nom. C'est pourquoi la racine (`@`) utilise des A records et `www` utilise un CNAME.

### MX — Mail Exchange
Indique quel serveur gère les **emails** pour ton domaine.
```
nemodzilla.xyz  →  mail.protonmail.ch  (priorité 10)
```

La priorité (nombre) détermine l'ordre de tentative — plus le nombre est bas, plus le serveur est prioritaire.

### TXT — Texte libre
Enregistrement texte libre, utilisé pour la **vérification de domaine** et les politiques email (SPF, DMARC).
```
nemodzilla.xyz  →  "v=spf1 include:_spf.google.com ~all"
```

---

## Sécurité email

### SPF — Sender Policy Framework
Un enregistrement **TXT** qui liste les serveurs autorisés à envoyer des emails en ton nom.
```
v=spf1 include:_spf.google.com ~all
```

- `include:` → serveurs autorisés
- `~all` → les autres sont suspects (soft fail)
- `-all` → les autres sont rejetés (hard fail)

Sans SPF, n'importe qui peut envoyer un email en se faisant passer pour `@nemodzilla.xyz`.

### DMARC — Domain-based Message Authentication
Politique qui dit aux serveurs de réception quoi faire si SPF/DKIM échouent.
```
v=DMARC1; p=reject; rua=mailto:dmarc@nemodzilla.xyz
```

- `p=none` → surveiller seulement
- `p=quarantine` → mettre en spam
- `p=reject` → rejeter l'email

### DKIM — DomainKeys Identified Mail
Signature cryptographique ajoutée aux emails pour prouver qu'ils viennent bien de toi. Configuré côté serveur mail, publié en TXT dans le DNS.

---

## Sécurité DNS

### DNSSEC
Ajoute des **signatures cryptographiques** aux enregistrements DNS pour éviter l'empoisonnement de cache (un attaquant qui redirige ton domaine vers une fausse IP).

Cloudflare peut l'activer en un clic : **DNS** → **DNSSEC** → Enable.

### CAA — Certification Authority Authorization
Définit quelles **autorités de certification** sont autorisées à émettre des certificats SSL pour ton domaine.
```
nemodzilla.xyz  CAA  0 issue "letsencrypt.org"
```

Empêche une CA malveillante d'émettre un certificat pour ton domaine à ton insu.

---

## Google Analytics & Tag Manager

### Google Analytics (GA4)
Outil de **mesure d'audience** — il te dit combien de visiteurs tu as, d'où ils viennent, quelles pages ils visitent, combien de temps ils restent.

L'ID ressemble à : `G-XXXXXXXXXX`

Pour l'activer sur Hugo Theme Stack, ajoute dans `params.toml` :
```toml
[analytics.google]
    id = "G-XXXXXXXXXX"
```

### Google Tag Manager (GTM)
Un **conteneur de scripts** qui permet d'ajouter/modifier des scripts de tracking (Analytics, pixels publicitaires, etc.) sans toucher au code du site.

L'ID ressemble à : `GTM-XXXXXXX`

La différence avec Analytics :
- **Analytics** → collecte et analyse les données
- **Tag Manager** → gère *comment* les scripts sont injectés dans la page

En pratique pour un site perso, Google Analytics seul suffit largement. Tag Manager est utile quand plusieurs outils de tracking coexistent et qu'on veut les gérer sans redéployer le site.

---

## Récapitulatif

| Enregistrement | Rôle |
|---------------|------|
| A | Domaine → IPv4 |
| AAAA | Domaine → IPv6 |
| CNAME | Domaine → autre domaine |
| MX | Domaine → serveur mail |
| TXT | Texte libre (SPF, DMARC, vérification) |
| CAA | Autorités SSL autorisées |
| DNSSEC | Signatures cryptographiques DNS |
| SPF | Serveurs mail autorisés |
| DMARC | Politique anti-usurpation email |