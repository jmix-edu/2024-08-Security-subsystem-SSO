=== Steps to integrate Keycloak users with JPA User entity

* Install OIDC add-on
* Remove dependency:

implementation 'io.jmix.authserver:jmix-authserver-starter'

* Add properties:

spring.security.oauth2.client.registration.keycloak.client-id=sample-sales-jmix
spring.security.oauth2.client.registration.keycloak.client-secret=ACTUAL_SECRET
spring.security.oauth2.client.registration.keycloak.scope=openid, profile, email
spring.security.oauth2.client.provider.keycloak.issuer-uri=http://localhost:8180/realms/master
jmix.oidc.use-default-jwt-configuration=false

* Remove properties 

spring.security.oauth2.authorizationserver.client.myclient.registration.client-id=hymwfnzizr
spring.security.oauth2.authorizationserver.client.myclient.registration.client-secret={noop}JociLIPfSs
spring.security.oauth2.authorizationserver.client.myclient.registration.authorization-grant-types=client_credentials
spring.security.oauth2.authorizationserver.client.myclient.registration.client-authentication_methods=client_secret_basic
spring.security.oauth2.authorizationserver.client.myclient.token.access-token-format=reference

* To associate a user from KeyCloak with the JPA User entity in Jmix, the entity must implement the JmixOidcUser interface, which inherits from OidcUser required by Spring Security. The easiest way to implement this interface is to inherit the entity from JmixOidcUserEntity.
  
Check the User.java

* To persist users and their roles in the database, we must extend SynchronizingOidcUserMapper. This abstract class can map an external user to the User entity from Jmix and save the user and role assignments in the database.

Check SalesSynchronizingOidcUserMapper.java

