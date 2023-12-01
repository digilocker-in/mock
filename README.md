## Digilocker Mock Server

Mock server for Digilocker APIs.

### Start

```bash
npm install
npm run start:dev
```

---

### Default configuration

<details>
  <summary>Click to expand</summary>

```ts
{
  issuer: 'http://localhost:3001',
  path: '/oidc',
  oidc: {
    clients: [
      {
        client_id: 'test',
        client_name: 'test',
        response_types: ['code'],
        token_endpoint_auth_method: 'none',
        application_type: 'web',
        redirect_uris: ['http://localhost:3001/callback'],
      },
    ],
    pkce: {
      methods: ['S256'],
      required: () => false,
    },
    scopes: [
      'openid',
      'offline_access',
      'profile',
      'email',
      'phone',
      'address'
    ],
    features: {
      devInteractions: {
        enabled: false,
      },
    },
    interactions: {
      url(_, interaction) {
        return `/interaction/${interaction.uid}`;
      },
    },
    cookies: {
      keys: [
        'gQMQym96H64-QInq7mvVX0nZEw0qUmcTA3bCpfnuR1h3YXNhgGJ0XLd17obmV8Gm',
      ],
    },
    jwks: {
      keys: [
        {
          kty: 'RSA',
          kid: 'UWXekTvfWi6o3wfYL9Wbd4f819MKevyQ0V4ksVn_YR0',
          use: 'sig',
          alg: 'RS256',
          e: 'AQAB',
          ...
        },
      ],
    },
  }
}
```

</details>

---

### Routes

#### Discovery: [/oidc/.well-known/openid-configuration](http://localhost:3001/oidc/.well-known/openid-configuration)

#### Authorization: [/oidc/auth](http://localhost:3001/oidc/auth?client_id=test&response_type=code&redirect_uri=http://localhost:3001/callback&scope=openid+email)

### References

1. [oidc-provider](https://github.com/adrianbrs/nest-oidc-provider)
