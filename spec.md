---
docname: draft-hanson-oauth-dyn-reg-rar-00
category: std

title: OAuth 2.0 Dynamic Client Registration Access using Rich Authorization Requests
author:
  -
    ins: J. Hanson
    name: Jared Hanson
    organization: Okta
    email: jared.hanson@okta.com

area: Security
workgroup: Web Authorization Protocol

--- abstract

This specification defines a mechanism by which an authorization server can
obtain end-user consent to permit dynamic registration of a client.  An OAuth
2.0 access token issued based on end-user consent can be used to limit the
parties that can register a client.

--- middle

# Introduction

OAuth 2.0 Dynamic Client Registration Protocol {{!RFC7591}} defines mechanisms
for dynamically registering OAuth 2.0 clients with authorization servers.  An
OAuth 2.0 access token can optionally be used to authorize calls to the client
registration endpoint.  However, the type and format of this token as well as
the means by which the authorization server issues it are out of scope of
{{!RFC7591}}.

This specification defines a mechanism using OAuth 2.0 Rich Authorization
Requests {{!I-D.ietf-oauth-security-topics}} by which an authorization can
obtain end-user consent to permit client registration.  The details regarding
the consent that was obtained can be communicated to the dynamic client
registration endpoint, which can be used to limit the parties that can register
a client as well as restrict allowable client metadata.

## Notational Conventions

{::boilerplate bcp14}

## Terminology

TODO

# Authorization Details Types

~~~~~~~~~~
  {
     "type": "client_registration",
     "actions": [
        "initiate",
        "status",
        "cancel"
     ],
     "locations": [
        "https://example.com/payments"
     ],
     "instructedAmount": {
        "currency": "EUR",
        "amount": "123.50"
     },
     "creditorName": "Merchant123",
     "creditorAccount": {
        "iban": "DE02100100109307118603"
     },
     "remittanceInformationUnstructured": "Ref Number Merchant"
  }
~~~~~~~~~~
