# Das ist ein begleitendes GitHub-Repository zum Artikel "Schluss mit Schlüsselchaos, Temporäre SSH-Schlüssel für Single Sign-on generieren", der in c't 22/2025 und [bei heise+](https://heise.de/-10639864) erschienen ist.

## Konfiguration des Client:

Login beim Identity-Provider und Generierung der Schlüssel:

```
opkssh login -i opkssh24h --provider="https://auth.example.com,Client-ID"
```

Persistente Konfigurationsdatei:

~/.opk/config.yml

```
---
default_provider: pocket-id

providers:
  - alias: pocket-id
    issuer: https://auth.example.com
    client_name: 'cttest'
    client_id: c451efee-d566-4359-876a-703014aacd97
    public: true
    require_pkce: true
    pkce_challenge_method: 'S256'
    scopes: openid email profile
    access_type: offline
    prompt: consent
    redirect_uris:
      - http://localhost:3000/login-callback
      - http://localhost:10001/login-callback
      - http://localhost:11110/login-callback
```

## Server-Konfiguration

Wer darf sich mit welchem Benutzer einloggen:

/etc/opkssh/auth-id
```
root cttest@example.com https://auth.example.com
```

Identity-Provider und Client ID eintragen:

/etc/opkssh/providers
```
https://auth.example.com c451efee-d566-4359-876a-703014aacd97 24h
```
