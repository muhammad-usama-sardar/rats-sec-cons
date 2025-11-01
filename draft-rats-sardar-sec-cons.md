---
title: "Guidelines for Security Considerations of RATS"
abbrev: "RATS Security Considerations"
category: info

docname: draft-rats-sardar-sec-cons-latest
updates: 9334
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
  Tech-Concepts:
     title: "Perspicuity of Attestation Mechanisms in Confidential Computing: Technical Concepts"
     date: October 2025,
     target: https://www.researchgate.net/publication/396199290_Perspicuity_of_Attestation_Mechanisms_in_Confidential_Computing_Technical_Concepts
     author:
      - ins: M. U. Sardar
  Gen-Approach:
     title: "Perspicuity of Attestation Mechanisms in Confidential Computing: General Approach"
     date: October 2025,
     target: https://www.researchgate.net/publication/396593308_Perspicuity_of_Attestation_Mechanisms_in_Confidential_Computing_General_Approach
     author:
      - ins: M. U. Sardar
  GDPR:
     title: "Regulation (EU) 2016/679 of the European Parliament and of
the Council of 27 April 2016 on the protection of natural persons with regard to the pro-
cessing of personal data and on the free movement of such data, and repealing Direc-
tive 95/46/EC (General Data Protection Regulation) (Text with EEA relevance)"
     date: May 4, 2016,
     target: https://eur-lex.europa.eu/eli/reg/2016/679/oj
     author:
      - ins: European Commission
  Dolev-Yao:
     title: "On the security of public key protocols"
     date: March 1983,
     author:
      - ins: D. Dolev
      - ins: A. Yao
  Foreshadow:
     title: "Perspicuity of Attestation Mechanisms in Confidential Computing: Technical Concepts"
     date: October 2025,
     target: https://foreshadowattack.eu/
     author:
      - ins: Jo Van Bulck
      - ins: Marina Minkin
      - ins: Ofir Weisse
      - ins: Daniel Genkin
      - ins: Baris Kasikci
      - ins: Frank Piessens
      - ins: Mark Silberstein
      - ins: Thomas F. Wenisch
      - ins: Yuval Yarom
      - ins: Raoul Strackx
  I-D.irtf-cfrg-cryptography-specification:
  I-D.deshpande-rats-multi-verifier:
  I-D.ietf-rats-coserv:

...

--- abstract

This document aims to provide guidelines and best practices for writing
   security considerations for technical specifications for RATS
   targeting the needs of implementers, researchers, and protocol
   designers. It presents an outline of the topics future versions will cover.


--- middle

# Introduction

While {{I-D.irtf-cfrg-cryptography-specification}} provides excellent guidelines, remote attestation {{-rfc9334}}
has several distinguishing features which necessitate a separate document.
One specific example of such feature is architectural complexity.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# General Hierarchy of Authentication
{{Gen-Approach}} proposes general hierarchy of one-way authentication, which can help precisely
state the intended level of authentication (in decreasing order):

* One-way injective agreement
* One-way non-injective agreement
* Aliveness

Recentness can be added to each of these levels of authentication.

# Threat Modeling

## System Model

## Actors

### Legal perspective

* Data subject is an identifiable natural person (as defined in Article 4 (1) of GDPR {{GDPR}}).
* (Data) Controller (as defined in Article 4 (7) of GDPR {{GDPR}}) manages and controls what happens with personal data of data subject.
* (Data) Processor (as defined in Article 4 (8) of GDPR {{GDPR}}) performs data processing on behalf of the data controller.


### Technical perspective

* Infrastucture Provider is a role which refers to the Processor in GDPR. An example of this role is a cloud service provider (CSP).

## Threat Model

## Typical Security Goals

# Attacks

Security considerations in RATS specifications need to clarify how the following attacks are avoided or mitigated:

* Diversion attacks: In this attack, a network adversary -- with Dolev-Yao capabilities {{Dolev-Yao}} and access (e.g., via
Foreshadow {{Foreshadow}}) to attestation key of any machine in the world -- can redirect a connection intended
for a specific Infrastructure Provider to the compromised machine, potentially resulting in exposure of
confidential data {{Meeting-122-TLS-Slides}}.
* Relay attacks
* Replay attacks

# Potential Mitigations

# Examples of Specifications That Could Be Improved

## RFC9334

### Unprotected Evidence
{{Section 7.4 of -rfc9334}} has:

{:quote}
>  A conveyance protocol that provides authentication and integrity protection can be used to convey Evidence that is otherwise unprotected (e.g., not signed).

Using a conveyance protocol that provides authentication and integrity protection, such as TLS 1.3 {{-rfc8446}},
to convey Evidence that is otherwise unprotected (e.g., not signed) undermines all security of remote attestation.
Essentially, this breaks the chain up to the trust anchor (such as hardware manufacturer) for remote attestation.
Hence, remote attestation effectively provides no protection in this case and the security guarantees are limited
to those of the conveyance protocol only. In order to benefit from remote attestation, Evidence MUST be protected
using dedicated keys chaining back to the trust anchor for remote attestation.

### Missing Roles and Conceptual Messages
* Identity Supplier and its corresponding conceptual message Identity are missing and need to be added to the architecture {{Tech-Concepts}}.
* Attestation Challenge as conceptual message needs to be added to the architecture {{Tech-Concepts}}.

# Examples of Parts of Specifications That Are Detrimental for Security

It is the author's personal opinion that the following parts of designs are detrimental for the RATS ecosystem:

* Multi-Verifiers {{I-D.deshpande-rats-multi-verifier}}: the design of multi-verifiers not only increases security risks
in terms of increasing the Trusted Computing Base (TCB), but also increases the privacy risks, as potentially sensitive
information is sent to multiple verifiers.

* Aggregator-based design {{I-D.ietf-rats-coserv}}: Aggregator is an explicit trust anchor and the addition of new
trust anchor needs to have a strong justification.


# Security Considerations

All of this document is about security considerations.



# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The author wishes to thank Ira McDonald and Ivan Gudymenko for insightful discussions.
The author also gratefully acknowledges the authors of {{I-D.irtf-cfrg-cryptography-specification}}, which
serves as the inspiration of this work.
