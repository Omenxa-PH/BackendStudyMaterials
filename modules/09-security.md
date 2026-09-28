# Module 09 — Spring Security, TLS, JWT, OAuth2, and OIDC

# Security Mental Model

Security is layered.

You need to think about:

- transport security
- authentication
- authorization
- credentials
- session/token lifecycle
- input validation
- secrets
- auditability

---

# Authentication vs Authorization

Authentication:

> Who are you?

Authorization:

> Are you allowed to do this?

---

# Password Storage

Do not store plaintext passwords.

Use a password-hashing algorithm designed for passwords.

In Spring Security, commonly use a `PasswordEncoder`.

---

# TLS / HTTPS

TLS provides:

- confidentiality in transit
- integrity
- server authentication

JWT does not replace TLS.

A signed token can still be stolen if sent over an insecure connection.

---

# mTLS

Mutual TLS authenticates both sides using certificates.

Common in:

- internal service-to-service security
- high-trust enterprise environments

---

# JWT

A JWT commonly contains:

```text
header.payload.signature
```

A signed JWT provides integrity/authenticity of claims.

It is not automatically encrypted.

Do not put secrets inside a normal signed JWT.

---

# Common JWT Claims

- `sub`
- `iss`
- `aud`
- `exp`
- `iat`
- `jti`

Validate:

- signature
- expiry
- issuer
- audience

---

# Access Token vs Refresh Token

## Access Token
Short-lived token used to call APIs.

## Refresh Token
Used to obtain a new access token.

Refresh tokens deserve stronger storage and rotation policies.

---

# OAuth2

OAuth2 is an authorization framework.

Roles:

- resource owner
- client
- authorization server
- resource server

Common flow:

- Authorization Code + PKCE for user-facing apps

For service-to-service:

- Client Credentials

---

# OpenID Connect

OIDC adds an identity layer on top of OAuth2.

It introduces concepts such as the ID Token.

---

# Spring Security Resource Server

Typical configuration:

```java
@Bean
SecurityFilterChain security(HttpSecurity http) throws Exception {
    return http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/actuator/health").permitAll()
            .requestMatchers("/admin/**").hasRole("ADMIN")
            .anyRequest().authenticated())
        .oauth2ResourceServer(oauth -> oauth.jwt())
        .build();
}
```

---

# Method Security

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) {
    ...
}
```

Use method-level authorization for business-sensitive operations where appropriate.

---

# CORS

CORS is a browser security mechanism.

It is not an authentication system.

Configure only trusted origins.

---

# CSRF

Especially relevant for cookie-based browser authentication.

Token-based APIs require threat-model-specific CSRF consideration depending on how credentials are stored and sent.

---

# Secrets

Never hard-code:

- DB passwords
- JWT keys
- API keys
- client secrets

Use:

- environment variables
- secret managers
- Kubernetes/OpenShift secrets

---

# Security Lab

Build:

- `/auth/login`
- access token
- refresh token
- `/profile`
- `/admin/**`

Requirements:

- hashed passwords
- short-lived access token
- refresh token rotation
- role authorization
- token expiry handling
- structured security logs

---

# Threat Exercise

For each, describe your mitigation:

1. stolen access token
2. leaked refresh token
3. replayed request
4. weak password
5. exposed signing key
6. overly broad CORS
7. privilege escalation
8. SQL injection
9. insecure admin endpoint
10. secrets accidentally committed to Git

---

# Interview Questions

1. Authentication vs authorization?
2. TLS vs JWT?
3. Is JWT encrypted?
4. OAuth2 vs OIDC?
5. Access vs refresh token?
6. What is PKCE?
7. What is Client Credentials?
8. What is CORS?
9. What is CSRF?
10. How would you rotate a signing key?
