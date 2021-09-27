# SSO Example using Micronaut 

## About: 
This project is for demonstrating the understanding of OAuth2.0, okta, and its use with in micronaut. 

This is based on the following documentation: https://guides.micronaut.io/latest/micronaut-oauth2-okta-maven-java.html

## Support: 

I will not provide support for this repo. 

## Setup: 

### Steps: 
 - Sign up at developer.okta.com and create a Web application with the following characteristics:
   - Check Authorization Code grant type.
   - Add http://localhost:8080/oauth/callback/okta as a login redirect URIs.
   - Add http://localhost:8080/logout as a Logout redirect URI.
   - Annotate the Client ID and Secret.
 
 - Add dependencies to maven: 
   - Add Micronaut Security 
   ```
   <dependency>
   <groupId>io.micronaut.security</groupId>
   <artifactId>micronaut-security-oauth2</artifactId>
   <scope>compile</scope>
   </dependency> 
   ```
   
   - Add Micronaut JWT Support: 
   ```
   <dependency>
    <groupId>io.micronaut.security</groupId>
    <artifactId>micronaut-security-jwt</artifactId>
    <scope>compile</scope>
    </dependency>
    ```
 - Add the following OAuth2 Configuration:
   src/main/resources/application.yml
    ``` 
   security:
    authentication: idtoken 
    oauth2:
      clients:
        okta: 
          client-secret: '${OAUTH_CLIENT_SECRET:yyy}' 
          client-id: '${OAUTH_CLIENT_ID:xxx}' 
          openid:
            issuer: '${OIDC_ISSUER_DOMAIN:`https://dev-XXXXX.oktapreview.com`}/oauth2/${OIDC_ISSUER_AUTHSERVERID:default}' 
    endpoints:
      logout:
        get-allowed: true 
   ```
 - Set Environment Variables: 
 
    ```
    export OAUTH_CLIENT_ID=XXXXXXXXXX
    export OAUTH_CLIENT_SECRET=YYYYYYYYYY
    export OIDC_ISSUER_DOMAIN=https://dev-XXXXX.oktapreview.com
    export OIDC_ISSUER_AUTHSERVERID=default
   ```
 - Run it 
