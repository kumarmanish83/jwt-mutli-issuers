# jwt-token-validation-policy-mule4

This policy is dependent on the JWT Validation module: (https://github.com/mulesoft-consulting/jwt-validation-module)

Publish your JWT validation module to the same organization that will host Custom Policy.
Reference the Module in pom.xml

```
<dependency>
			<groupId>${org_id}</groupId>
			<artifactId>jwt-validation</artifactId>
			<version>1.0.0</version>
			<classifier>mule-plugin</classifier>
</dependency>
```

### Specs

Policy supports these algorithms for digital signature verification:

- HS256,HS384,HS512
- RS256,RS384,RS512
- ES256,ES384,ES512

This policy requires Java 8

HTTP Authorization header must have following form:

```
Bearer <jwt>
```

like this example:
```
Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

### The policy currently can validate the following fields:
1. Authorization Header
2. validate dynamic Issuers(upto 2)
3. Audience
4. Scopes (scopes need to be provided in a comma separated format, for example: gold, silver)
5. Expiration (default true)
6. Not before (default false, Verifies that the token is not being consumed before 'nbf' claim only if it is present)
7. Allow unsecured Tokens (default false)


### User has to provide:
1. Either the Public Certificate
2. Or provide the details of the service from where the keys can be retrieved (host, basepath). This uses HTTPs service as a default.
