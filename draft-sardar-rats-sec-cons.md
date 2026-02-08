---
title: "Guidelines for Security Considerations of RATS"
abbrev: "RATS Security Considerations"
category: info

docname: draft-sardar-rats-sec-cons-latest
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
  latest: "https://muhammad-usama-sardar.github.io/rats-sec-cons/draft-sardar-rats-sec-cons.html"

author:
 -
    fullname: "Muhammad Usama Sardar"
    organization: TU Dresden
    email: "muhammad_usama.sardar@tu-dresden.de"

normative:
  RFC9334: rfc9334
  RFC9781: rfc9781
  RFC9711: rfc9711
  RFC9783: rfc9783

informative:
  RFC8446: rfc8446
  RFC3552: rfc3552
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
     title: "Foreshadow"
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
  Clarifications-EAT:
     title: "Clarifications in draft-ietf-rats-eat"
     date: 11 April 2025,
     target: https://mailarchive.ietf.org/arch/msg/rats/4V2zZHhk5IuxwcUMNWpPBpnzpaM/
     author:
     - ins: M. U. Sardar
  Sec-Cons-RATS:
     title: "Security considerations of remote attestation (RFC9334)"
     date: 25 November 2024,
     target: https://mailarchive.ietf.org/arch/msg/rats/jcAv9FKbYSIVtUNQ8ggEHL8lrmM/
     author:
     - ins: M. U. Sardar
  RA-TLS:
    title: "Towards Validation of TLS 1.3 Formal Model and Vulnerabilities in Intel's RA-TLS Protocol"
    date: 13 November 2024,
    target: https://www.researchgate.net/publication/385384309_Towards_Validation_of_TLS_13_Formal_Model_and_Vulnerabilities_in_Intel's_RA-TLS_Protocol
    author:
      - ins: M. U. Sardar
      - ins: A. Niemi
      - ins: H. Tschofenig
      - ins: T. Fossati
  RelayAttacks-RATS:
     title: "Relay Attacks in Intra-handshake Attestation for Confidential Agentic AI Systems"
     date: 11 January 2026,
     target: https://mailarchive.ietf.org/arch/msg/rats/6gbqx0XY8WYrH3Mx4vO8n2-uKgY/
     author:
     - ins: M. U. Sardar
  ID-Crisis:
    title: "Identity Crisis in Confidential Computing: Formal Analysis of Attested TLS"
    date: November 2025,
    target: https://www.researchgate.net/publication/398839141_Identity_Crisis_in_Confidential_Computing_Formal_Analysis_of_Attested_TLS
    author:
      - ins: M. U. Sardar
      - ins: M. Moustafa
      - ins: T. Aura
  ID-Crisis-Repo:
     title: "Identity Crisis in Confidential Computing: Formal analysis of attested TLS protocols"
     date: 2025,
     target: https://github.com/CCC-Attestation/formal-spec-id-crisis
     author:
      - ins: Muhammad Usama Sardar
  Usama-TLS-26Feb25:
     title: "Impersonation attacks on protocol in draft-fossati-tls-attestation (Identity crisis in Attested TLS) for Confidential Computing"
     date: 26 February 2025,
     target: https://mailarchive.ietf.org/arch/msg/tls/Jx_yPoYWMIKaqXmPsytKZBDq23o/
     author:
      - ins: Muhammad Usama Sardar
  I-D.ietf-tls-rfc8446bis:
  RFC9261: rfc9261
  RFC9266: rfc9266

...

--- abstract

This document aims to provide guidelines and best practices for writing
   security considerations for technical specifications for RATS
   targeting the needs of implementers, researchers, and protocol
   designers. This is a work-in-progress, and the current version mainly presents an outline of the topics that future versions
   will cover in more detail.

* Corrections in published RATS RFCs
* Security concerns in two RATS drafts
* General security guidelines, baseline, or template for RATS

--- middle

# Introduction

## Need for Specialized Guidance in RATS
Every Internet Draft needs to have a "Security Considerations" section.
While general guidelines such as {{-rfc3552}} exist, the underlying threat model is that
the endpoint is fully trusted (i.e., all software and hardware components in the device may access the keys).
RATS {{-rfc9334}} has a primarily different threat model in the sense that only parts of the endpoint (called Attester) are trusted (i.e., only specific software and hardware components in the device may access the keys), and the goal is to establish the trustworthiness of the endpoint.
In other words, {{-rfc3552}} deals with a network adversary, whereas RATS deals with an endpoint adversary, which may have root access or physical control over the device with which it can extract keys from software or hardware.

Moreover, remote attestation has several distinguishing features that necessitate a separate document.
One specific example of such a feature is the architectural complexity of the endpoint.
While network protocols typically have 2 roles, RATS has additional roles, which complicates
the picture.
Unfortunately, no guidelines currently exist for remote attestation {{-rfc9334}} in RATS.
This document aims to fill this gap.

## Needs of the Target Audience of RATS
Moreover, while the target audience of Internet Drafts is implementers, researchers, and protocol designers {{I-D.irtf-cfrg-cryptography-specification}}, RATS drafts generally do not fulfill these needs, in particular the needs of researchers and protocol designers.
On the other hand, in our observation, implementers generally find it hard to relate the abstract concepts of RATS to the real-world systems. In general, implementers and protocol designers of RATS are thus left with little or no guidance.

## Inaccuracies in Published RATS RFCs
Unfortunately, many published RFCs of RATS provide inaccurate or ambiguous security and privacy considerations, which may lead to errors in design and implementation, and give a false
sense of security.
As an example, many proposed designs in {{-rfc9334}} are broken.

## Aggregator in CoServ
RATS has recently adopted {{I-D.ietf-rats-coserv}}, which has an ambiguous role Aggregator, for which -- in our assessment -- the authors have not yet provided a reasonable justification.
To the best of our knowledge and understanding, a malicious Aggregator breaks the security of the RATS ecosystem and invalidates the formal proofs for RATS primitives.
Surprisingly, during the three-week adoption call and one week discussion afterwards, one of the authors of the draft {{I-D.ietf-rats-coserv}} did not support adoption of the draft. Based on the above reasons, as researchers, we have genuine skepticism about this work. We request the authors to be transparent on this work and clarify the concerns raised at the adoption time (summarized to some extent in this draft).

## Scope
To improve the situation, this draft presents an outline of three topics that future versions will cover in more detail:

* Corrections in published RATS RFCs {{-rfc9334}}, {{-rfc9781}}, {{-rfc9783}} and {{-rfc9711}}
* Security concerns in one currently adopted RATS draft {{I-D.ietf-rats-coserv}} and one proposed for
adoption RATS draft {{I-D.deshpande-rats-multi-verifier}}
* General security baseline that other drafts can simply point to, or guidelines or template that other drafts can use


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# General Hierarchy of Authentication
Authentication is a term which is often ambiguous in RATS specifications. We propose general hierarchy of one-way authentication {{Gen-Approach}}, which can help precisely
state the intended level of authentication (in decreasing order):

* One-way injective agreement
* One-way non-injective agreement
* Aliveness

Recentness can be added to each of these levels of authentication.
Details will be added in future versions.

# Threat Modeling
This section describes "What can go wrong?" TODO.

## System Model
TODO.

## Actors
TODO.

### Legal perspective

* Data subject is an identifiable natural person (as defined in Article 4 (1) of GDPR {{GDPR}}).
* (Data) Controller (as defined in Article 4 (7) of GDPR {{GDPR}}) manages and controls what happens with personal data of data subject.
* (Data) Processor (as defined in Article 4 (8) of GDPR {{GDPR}}) performs data processing on behalf of the data controller.

TODO.

### Technical perspective

* Infrastucture Provider is a role which refers to the Processor in GDPR. An example of this role is a cloud service provider (CSP).

TODO.

## Threat Model
TODO.

## Typical Security Goals
TODO.

# Attacks

Security considerations in RATS specifications need to clarify how the following attacks are avoided or mitigated:

## (Evidence) Replay Attacks
In this attack, a network or endpoint adversary -- with access to older Evidence -- can replay Evidence with stale Claims which no longer represent the actual state of the Attester, potentially resulting in exposure of confidential data {{RA-TLS}}.

Replay of stale Evidence may be within the same connection or across multiple connections.

## Diversion Attacks
In this attack, a network adversary -- with Dolev-Yao capabilities {{Dolev-Yao}} and access (e.g., via
Foreshadow {{Foreshadow}}) to the attestation key of any machine in the world -- can redirect a connection intended
for a specific Infrastructure Provider to the compromised machine, potentially resulting in exposure of
confidential data {{ID-Crisis}}.

In the context of confidential computing and TLS as a transport protocol, we reported these attacks to the TLS WG in February 2025 {{Usama-TLS-26Feb25}}. A formal proof is available
{{ID-Crisis-Repo}} for further research and
development. Since reporting to TLS WG, these attacks have been practically
exploited in [TEE.fail](https://tee.fail/), [Wiretap.fail](https://wiretap.fail/), and [BadRAM](https://badram.eu/).

## Relay Attacks
In this attack, a network or endpoint adversary -- with access to suitable binding material -- can relay an attestation request to a genuine Attester and present the genuine Evidence as its own,
potentially resulting in impersonation of genuine Attester {{RelayAttacks-RATS}}.

Note that *replay* is about *same* Attester while *relay* attack is about *different* Attesters.

# Potential Mitigations
This section describes the countermeasures and their evaluation.

To mitigate the above attacks, we propose post-handshake attestation.
We are not aware of any attacks on post-handshake attestation. Post-handshake attestation
avoids replay attacks by using a fresh attestation nonce. Moreover, considering TLS as the transport protocol, it avoids diversion and relay attacks
by binding the Evidence to the underlying TLS connection, such as using Exported Keying Material (EKM)
{{I-D.ietf-tls-rfc8446bis}}, as proposed in Section 9.2 of {{ID-Crisis}}. {{-rfc9261}} and {{-rfc9266}} provide mechanisms for such bindings. Efforts for a formal proof
of security of post-handshake attestation are ongoing.

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

### Missing definitions
{{-rfc9334}} uses the term Conceptual Messages in capitalization without proper definition.

### Missing Roles and Conceptual Messages
* Identity Supplier and its corresponding conceptual message Identity are missing and need to be added to the architecture {{Tech-Concepts}}.
* Attestation Challenge as conceptual message needs to be added to the architecture {{Tech-Concepts}}.

## RFC9781

As argued above for RFC9334, security considerations in {{-rfc9781}} are essentially insufficient.

## RFC9783
{{-rfc9783}} uses:

* 3x epoch handle (with reference to {{Section 10.2 of -rfc9334}} and
{{Section 10.3 of -rfc9334}}) whereas RFC9334 never uses epoch handle at all!
* 1x epoch ID with no reference and no explanation of how it is
    different from epoch handle

## RFC9711

### Inaccurate opinion

{{Section 7.4 of -rfc9711}} has:

{:quote}
>  For attestation, the keys are associated with specific devices and are configured by device manufacturers.

The quoted text is inaccurate and just an opinion of the editors.
It should preferably be removed from the RFC.
For example, in SGX, the keys are not configured by the manufacturer alone.
The platform owner can provide a random value called OWNER_EPOCH.

For technical details and proposed text, see {{Clarifications-EAT}}.

### Inaccurate Privacy Considerations

{{Section 8.4 of -rfc9711}} has:

{:quote}
>
The nonce claim is based on a value usually derived remotely (outside of the entity).

Attester-generated nonce does not provide any replay protection since the Attester can pre-generate an Evidence
that might not reflect the actual system state, but a past one.

See the attack trace for Attester-generated nonce at {{Sec-Cons-RATS}}.

For replay protection, nonce should *always* be derived remotely (for example, by the Relying Party).

# Examples of Parts of Specifications That are Detrimental for Security

We believe that the following parts of designs are detrimental for the RATS ecosystem:

## Multi-Verifiers

### Security Considerations
We believe the security considerations of multi-verifiers {{I-D.deshpande-rats-multi-verifier}} must say:

Compared to a single verifier, the use of multi-verifiers increases security risks in terms of increasing the Trusted Computing Base (TCB).

### Privacy Considerations
We believe the privacy considerations of multi-verifiers {{I-D.deshpande-rats-multi-verifier}} should say:

Compared to a single verifier, the use of multi-verifiers may increase the privacy risks, as potentially sensitive information may be sent to multiple verifiers.

### Open-source
Besides, the rationale presented by the authors at meeting 124 -- appraisal policy being the intellectual property of the vendors -- breaks the
open-source nature of RATS ecosystem. This requires blindly trusting the vendors and increases the attack surface.

## Aggregator-based design
Aggregator in {{I-D.ietf-rats-coserv}} is an explicit trust anchor and the addition of new trust anchor needs to have a strong justification.
Having a malicious Aggregator in the design trivially breaks all the guarantees.
It should be clarified how trust is established between Aggregator and Verifier in the context of Confidential Computing threat model.

The fact that Aggregator has collective information of Reference Values Providers and Endorsers
makes it a special target of attack, and thus a single point of failure. It increases security
risks because Aggregator can be compromised independent of the Reference Values Providers and
Endorsers. That is, even if Reference Values Providers and Endorsers are secure, the compromise
of Aggregator breaks the security of the system.
Moreover, if Aggregator is not running inside a TEE, it is relatively easy to compromise the secrets.


# Security Considerations

All of this document is about security considerations.



# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The author wishes to thank Ira McDonald and Ivan Gudymenko for insightful discussions.
The author also wishes to thank the authors of {{I-D.ietf-rats-coserv}} (in particular Thomas
Fossati and Paul Howard) for several discussions, which unfortunately could not resolve the
above concerns, and hence led to this draft.

# History
{:numbered="false"}

-01

* Concrete text proposal for security and privacy considerations of multi-verifiers {{I-D.deshpande-rats-multi-verifier}}

-02

* Introduction and motivation
* Defined replay and relay attacks
* Added mitigations
