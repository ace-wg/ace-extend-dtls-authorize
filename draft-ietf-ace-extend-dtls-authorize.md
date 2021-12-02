---
title: Extension of the ACE CoAP-DTLS Profile to TLS 
docname: draft-bergmann-ace-extend-dtls-authorize
abbrev: CoAP-DTLS Extension
updates: draft-ietf-ace-dtls-authorize
ipr: trust200902
cat: std

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

  RFC7252:
  RFC8323:
  RFC8446:
  I-D.ietf-tls-dtls13:
  I-D.ietf-ace-dtls-authorize:

informative:

  RFC7525:
  RFC8996:
  I-D.ietf-ace-oscore-profile:

--- abstract

This document updates the ACE CoAP-DTLS profile by specifying that the profile applies to TLS as well as DTLS.

--- middle

# Introduction

{{I-D.ietf-ace-dtls-authorize}} only specifies use of DTLS {{I-D.ietf-tls-dtls13}} but works equally well for TLS. For many constrained implementations, CoAP over UDP {{RFC7252}} is the first choice, but when deploying ACE in networks controlled by other entities (such as the Internet), UDP might be blocked on the path between the client and the RS, and the client might have to fall back to CoAP over TCP {{RFC8323}} for NAT or firewall traversal. This feature is supported by the OSCORE profile {{I-D.ietf-ace-oscore-profile}} but is lacking from the DTLS profile.

This document updates {{I-D.ietf-ace-dtls-authorize}} by specifying that the profile applies to TLS as well as DTLS. The same access token is valid for both DTLS or TLS. The access rights do not depend on the transport layer security.

# IANA Considerations

No IANA Considerations.

# Security Considerations

The security consideration and requirements in TLS 1.3 {{RFC8446}} and BCP 195 {{RFC7525}} {{RFC8996}} also apply to this document.

--- back

# Acknowledgments
{: numbered="no"}


--- fluff
