# opkssh-passkeys

## Client

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

## Server

/etc/opkssh/auth-id
```
root b1d50729-5ad5-42e6-b34c-d0c7142ef6d0 https://auth.example.com
```

/etc/opkssh/providers
```
https://auth.example.com c451efee-d566-4359-876a-703014aacd97 24h
```
