---
title: "Guidelines for Security Considerations of RATS"
abbrev: "RATS Security Considerations"
category: info

docname: draft-rats-sardar-sec-cons-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
# area: AREA
workgroup: RATS Working Group
keyword:
 - security considerations
 - remote attestation
venue:
#  group: WG
#  type: Working Group
#  mail: WG@example.com
#  arch: https://example.com/WG
  github: "muhammad-usama-sardar/rats-sec-cons"
  latest: "https://muhammad-usama-sardar.github.io/rats-sec-cons/draft-rats-sardar-sec-cons.html"

author:
 -
    fullname: "Muhammad Usama Sardar"
    organization: TU Dresden
    email: "muhammad_usama.sardar@tu-dresden.de"

normative:
  RFC9334: rfc9334

informative:
  RFC8446: rfc8446
  Meeting-122-TLS-Slides:
     title: "Identity Crisis in Attested TLS for Confidential Computing"
     date: 20 March 2025,
     target: https://datatracker.ietf.org/meeting/122/materials/slides-122-tls-identity-crisis-00
     author:
     - ins: M. U. Sardar
     - ins: M. Moustafa
     - ins: T. Aura


...

--- abstract

This document provides guidelines and best practices for writing
   technical specifications for RATS targeting the needs of implementers, researchers, and protocol
   designers.


--- middle

# Introduction

TODO Introduction


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Examples of Specifications That Could Be Improved

## RFC9334

### Unprotected Evidence
{{Section 7.4 of -rfc9334}} has:

{:quote}
>  A conveyance protocol that provides authentication and integrity protection can be used to convey Evidence that is otherwise unprotected (e.g., not signed).

Using a conveyance protocol that provides authentication and integrity protection, such as TLS 1.3 {{-rfc8446}}, to convey Evidence that is otherwise unprotected (e.g., not signed) undermines all security of remote attestation. Essentially, this breaks the chain up to the trust anchor (such as hardware manufacturer) for remote attestation. Hence, remote attestation effectively provides no protection in this case and the security guarantees are limited to those of the conveyance protocol only. In order to benefit from remote attestation, Evidence MUST be protected using dedicated keys chaining back to the trust anchor for remote attestation.

### Missing Roles
* Identity Supplier and its corresponding conceptual message Identity are missing need to be added to the architecture {{Meeting-122-TLS-Slides}}.
* Attestation Challenge as conceptual message needs to be added to the architecture.

# Security Considerations

All of this document is about security considerations.



# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The author wishes to thank Ira McDonald for insightful discussion.
