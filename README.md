# JHipster 6.5.1 Authentication With Azure Active Directory

This application was generated using JHipster 6.5.1, you can find documentation and help at [https://www.jhipster.tech/documentation-archive/v6.5.1](https://www.jhipster.tech/documentation-archive/v6.5.1).

This is a "gateway" application intended to be part of a microservice architecture, please refer to the [Doing microservices with JHipster][] page of the documentation for more information.

This application is configured for Service Discovery and Configuration with . On launch, it will refuse to start if it is not able to connect to .

The authentication type is oauth2.

## Before Run

This is the tutorial Link https://dev.to/azure/using-spring-security-with-azure-active-directory-mga
by Julien Dubois

# FOLLOW THE TUTORIAL FIRST

Follow the tutorial before clone this project.

Go to src/main/resources/application.yml and change the following

# Spring security Oauth2
spring:
  security:
    oauth2:
      client:
        registration:
          azure:
            client-id: <<CLIENT_ID>>
            client-secret: <<CLIENT_SECRET>>
'
# Azure Activedirectory configuration
'
azure:
  activedirectory:
    tenant-id: <<YOUR_TENANT_ID>>
    active-directory-groups: Users
  b2c:
    reply-url: http://localhost:9000 # should be absolute url.
    logout-success-url: http://localhost:9000
'
# Edited file from original JHipster:

* SecurityConfiguration.java
* LogoutResource.java
    * From this.registration = registrations.findByRegistrationId("oidc");
    * To this.registration = registrations.findByRegistrationId("azure");
    * Change is in logout method because
        this.registration.getProviderDetails().getConfigurationMetadata().get("end_session_endpoint") is null
* login.service.ts
    * From location.href = `${location.origin}${this.location.prepareExternalUrl('oauth2/authorization/oidc')}`;
    * TO location.href = `${location.origin}${this.location.prepareExternalUrl('oauth2/authorization/azure')}`;
