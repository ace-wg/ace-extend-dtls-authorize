---
title: Extension of the Datagram Transport Layer Security (DTLS) Profile for Authentication and Authorization for Constrained Environments (ACE) to Transport Layer Security (TLS)
docname: draft-ietf-ace-extend-dtls-authorize
abbrev: CoAP-DTLS Extension to TLS
docname: draft-ietf-ace-extend-dtls-authorize-latest
updates: 9202
ipr: trust200902
cat: std
workgroup: ACE Working Group
stream: IETF

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
  RFC9147:
  RFC9200:
  RFC9202:

informative:

  RFC8996:
  RFC9203:
  RFC9325:

entity:
        SELF: "[RFC-XXXX]"

--- abstract

This document updates the Datagram Transport Layer Security (DTLS) Profile for Authentication and Authorization for Constrained Environments (ACE) specified in RFC 9202 by specifying that the profile applies to Transport Layer Security (TLS) as well as Datagram TLS (DTLS).

--- middle

# Introduction 

The Authentication and Authorization for Constrained Environments (ACE) framework {{RFC9200}} defines an architecture for lightweight authentication between Client, Resource Server (RS), Authorization Server (AS) where the Client and RS may be constrained. The Datagram Transport Layer Security (DTLS) Profile for Authentication and Authorization for Constrained Environments (ACE) {{RFC9202}} only specifies the use of Datagram Transport Layer Security (DTLS) {{RFC9147}} for transport-layer security between the nodes in the ACE architecture but works equally well for Transport Layer Security (TLS) {{RFC8446}}. For many constrained implementations, Constrained Application Protocol (CoAP) over UDP {{RFC7252}} is the first choice, but when deploying ACE in networks controlled by other entities (such as the Internet), UDP might be blocked on the path between the Client and the RS, and the Client might have to fall back to CoAP over TCP {{RFC8323}} for NAT or firewall traversal. This dual support for security over TCP as well as UDP is already supported by the Object Security for Constrained RESTful Environments (OSCORE) profile {{RFC9203}}.

This document updates {{RFC9202}} by specifying that the profile applies to TLS as well as DTLS. It only impacts the transport layer security channel between Client and Resource Server. The same access rights are valid in case transport layer security is provided by either DTLS or TLS. The same access token can be used by either DTLS or TLS between a given (Client, RS) pair. Therefore, the value `coap_dtls` in the `ace_profile` parameter of an Authorization Server to Client (AS-to-Client) response or in the `ace_profile` claim of an access token indicates that either DTLS or TLS can be used for transport layer security.


# Terminology

{::boilerplate bcp14-tagged}

Readers are expected to be familiar with the terms and concepts
described in {{RFC9200}} and {{RFC9202}}.

# Specific Changes to RFC 9202

The main changes to {{RFC9202}} specified in this document are limited
to replacing "DTLS" with "DTLS/TLS" throughout the document. This
essentially impacts the use of secure transport as described in the
sections 3.2.2, 3.3.2, 4, and 5.

In addition to this, the Client and Resource Server behavior is
updated to describe the case where either or both DTLS and TLS may be
available, as described in the following section.

# Connection Establishment

Following the procedures defined in {{RFC9202}}, a
Client can retrieve an Access Token from an Authorization Server (AS)
in order to establish a security association with a specific Resource
Server. The `ace_profile` parameter in the Client-to-AS request and
AS-to-client response is used to determine the ACE profile that the
Client uses towards the Resource Server (RS).

The `ace_profile` parameter indicates the use of the DTLS
profile for ACE as defined in {{RFC9202}}. Therefore, the Client typically
first tries using DTLS to connect to the Resource Server. If this fails the
Client MAY try to connect to the Resource Server via TLS.

As resource-constrained devices are not expected to support both
transport layer security mechanisms, Clients and Resource Servers
SHOULD support DTLS and MAY support TLS. A Client that implements either
TLS or DTLS but not both might fail in establishing a secure
communication channel with the Resource Server altogether. Non-constrained
Clients and Resource Servers SHOULD support both TLS and DTLS.

Note that a communication setup with an a priori unknown Resource
Server typically employs an initial unauthorized resource request as
illustrated in Section 2 of {{RFC9202}}. If this
message exchange succeeds, the Client SHOULD first use the same
underlying transport protocol also for the establishment of the security
association to RS (i.e., DTLS for UDP, and TLS for TCP).

As a consequence, the selection of the transport protocol used for the
initial unauthorized resource request also depends on the transport
layer security mechanism supported by the Client.  Clients that
support either DTLS or TLS but not both SHOULD use the transport
protocol underlying the supported transport layer security mechanism
also for an initial unauthorized resource request to the RS as in Section 2 of {{RFC9202}}.

# IANA Considerations

The following updates have been done to the "ACE Profiles" registry
for the profile with a "CBOR Value" field value of 1 and "Name" of "coap_dtls":

Note to RFC Editor: Please replace all occurrences of "{{&SELF}}" with
the RFC number of this specification and delete this paragraph.

Description: Profile for delegating client Authentication and
Authorization for Constrained Environments by establishing a Datagram
Transport Layer Security (DTLS) or Transport Layer Security (TLS)
channel between resource-constrained nodes.

Change Controller:  IESG

Reference:  \[RFC9202\] {{&SELF}}

# Security Considerations

The security consideration and requirements in {{RFC9202}}, TLS 1.3 {{RFC8446}}, and BCP 195 {{RFC8996}} {{RFC9325}} also apply to this document.

--- back

# Acknowledgments
{: numbered="no"}

The authors would like to thank Marco Tiloca for reviewing this
specification.

--- fluff
