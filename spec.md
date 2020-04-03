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
Requests {{!I-D.ietf-oauth-rar}} by which an authorization can
obtain end-user consent to permit client registration.  The details regarding
the consent that was obtained can be communicated to the dynamic client
registration endpoint, which can be used to limit the parties that can register
a client as well as restrict allowable client metadata.

## Notational Conventions

{::boilerplate bcp14}

## Terminology

TODO

# Authorization Data Type

To make an authorization request for client registration, the client makes an
authorization request as defined in Section 3.1 of OAuth 2.0 Rich Authorization
Requests {{!I-D.ietf-oauth-rar}}.

This value of the `type` of the authorization object is `client_registration`.

The authorization object can contain any of the common data elements defined in
Section 2.1 of {{!I-D.ietf-oauth-rar}} or any of the client metadata fields
defined in Section 2 of OAuth 2.0 Dynamic Client Registration Protocol
{{!RFC7591}}.  The implementation and use of all fields is OPTIONAL, unless
stated otherwise.

For example, a client registration authorization object could contain the
following fields:

~~~~~~~~~~
  [
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
      "redirect_uris": [
        "https://client.example.org/callback",
        "https://client.example.org/callback2"
      ],
      "client_name": "My Example Client",
      "client_name#ja-Jpan-JP":
         "\u30AF\u30E9\u30A4\u30A2\u30F3\u30C8\u540D",
      "token_endpoint_auth_method": "client_secret_basic",
      "logo_uri": "https://client.example.org/logo.png",
      "jwks_uri": "https://client.example.org/my_public_keys.jwks",
      "example_extension_parameter": "example_value"
    }
  ]
~~~~~~~~~~
