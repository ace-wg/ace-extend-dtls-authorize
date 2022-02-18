---
title: Extension of the CoAP-DTLS Profile for ACE to TLS
docname: draft-ietf-ace-extend-dtls-authorize
abbrev: CoAP-DTLS Extension
docname: draft-ietf-ace-extend-dtls-authorize-latest
updates: draft-ietf-ace-dtls-authorize
ipr: trust200902
cat: std
workgroup: ACE Working Group

coding: utf-8
pi: # can use array (if all yes) or hash here
  toc: yes
  sortrefs: yes
  symrefs: yes
  tocdepth: 2

author:
- name: Olaf Bergmann
  surname: Bergmann
  org: Universität Bremen TZI
  abbrev: TZI
  street: Bremen, D-28359
  country: Germany
  email: bergmann@tzi.org
- name: John Preuß Mattsson
  initials: J
  surname: Preuß Mattsson
  org: Ericsson AB
  abbrev: Ericsson
  street: SE-164 80 Stockholm
  country: Sweden
  email: john.mattsson@ericsson.com
- name: Göran Selander
  surname: Selander
  org: Ericsson AB
  abbrev: Ericsson
  street: SE-164 80 Stockholm
  country: Sweden
  email: goran.selander@ericsson.com


normative:

  RFC6347:
  RFC7252:
  RFC8323:
  RFC8446:
  I-D.ietf-tls-dtls13:
  I-D.ietf-ace-dtls-authorize:

informative:

  RFC7525:
  RFC8996:
  I-D.ietf-ace-oscore-profile:

entity:
        SELF: "[RFC-XXXX]"

--- abstract

This document updates the CoAP-DTLS profile for ACE {{I-D.ietf-ace-dtls-authorize}} by specifying that the profile applies to TLS as well as DTLS.

--- middle

# Introduction

{{I-D.ietf-ace-dtls-authorize}} only specifies the use of DTLS {{RFC6347}} but works equally well for TLS {{RFC8446}}. For many constrained implementations, CoAP over UDP {{RFC7252}} is the first choice, but when deploying ACE in networks controlled by other entities (such as the Internet), UDP might be blocked on the path between the client and the RS, and the client might have to fall back to CoAP over TCP {{RFC8323}} for NAT or firewall traversal. This feature is supported by the OSCORE profile {{I-D.ietf-ace-oscore-profile}} but is lacking in the DTLS profile.

This document updates {{I-D.ietf-ace-dtls-authorize}} by specifying that the profile applies to TLS as well as DTLS. The same access rights are valid in case transport layer security is provided by either DTLS or TLS, and the same access token can be used.
Therefore, the value `coap_dtls` in the `ace_profile` parameter of an
AS-to-Client response or in the `ace_profile` claim of an access token
indicates that either DTLS or TLS can be used for transport layer
security.


# IANA Considerations

The following updates are done to the ACE OAuth Profile Registry for
the profile with Profile ID 1 and Profile name coap_dtls:

Note to RFC Editor: Please replace all occurrences of "{{&SELF}}" with
the RFC number of this specification and delete this paragraph.

Profile Description: Profile for delegating client authentication and
authorization in a constrained environment by establishing a Datagram
Transport Layer Security (DTLS) or Transport Layer Security (TLS)
channel between resource-constrained nodes.

Change Controller:  IESG

Reference:  {{&SELF}}

# Security Considerations

The security consideration and requirements in TLS 1.3 {{RFC8446}} and BCP 195 {{RFC7525}} {{RFC8996}} also apply to this document.

--- back

# Acknowledgments
{: numbered="no"}


--- fluff
