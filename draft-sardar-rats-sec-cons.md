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
 -
    fullname: "Songbo Bu"
    organization: Stevens Institute of Technology
    city: New York
    country: USA
    email: "bluedognull@gmail.com"
 -
    fullname: "Chengxin Huang"
    organization: Independent
    email: "aurestarnull@gmail.com"
 -
    fullname: "Haowen Song"
    organization: Shanghai Guan An Information Technology Co., Ltd.
    country: China
    email: "havan12050544@gmail.com"

normative:
  RFC9334: rfc9334

informative:
  RFC3552: rfc3552
  GDPR:
     title: "Regulation (EU) 2016/679 of the European Parliament and of the Council of 27 April 2016 on the protection of natural persons with regard to the processing of personal data and on the free movement of such data, and repealing Directive 95/46/EC (General Data Protection Regulation) (Text with EEA relevance)"
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
  RA-TLS:
    title: "Towards Validation of TLS 1.3 Formal Model and Vulnerabilities in Intel's RA-TLS Protocol"
    date: 13 November 2024,
    target: https://www.researchgate.net/publication/385384309_Towards_Validation_of_TLS_13_Formal_Model_and_Vulnerabilities_in_Intel's_RA-TLS_Protocol
    author:
      - ins: M. U. Sardar
      - ins: A. Niemi
      - ins: H. Tschofenig
      - ins: T. Fossati
  ID-Crisis: DOI.10.1145/3779208.3785387
  ID-Crisis-repo:
    title: "Identity Crisis in Confidential Computing: Formal Analysis of Attested TLS"
    date: November 2025,
    target: https://github.com/CCC-Attestation/formal-spec-id-crisis
    author:
      - ins: M. U. Sardar
      - ins: M. Moustafa
      - ins: T. Aura
  Intra-handshake.fail:
    title: "Intra-handshake.fail (CVE-2026-33697): High-severity CVE in Attested TLS"
    date: June 2026,
    target: https://www.researchgate.net/publication/408219182_Intra-handshakefail_CVE-2026-33697_High-severity_CVE_in_Attested_TLS
    author:
      - ins: M. U. Sardar
      - ins: V. Dubeyko
      - ins: J-M. Jacquet
  Intra-handshake.fail-repo:
    title: "Intra-handshake.fail (CVE-2026-33697): High-severity CVE in Attested TLS"
    date: June 2026,
    target: https://github.com/CCC-Attestation/formal-spec-KBS
    author:
      - ins: M. U. Sardar
      - ins: V. Dubeyko
      - ins: J-M. Jacquet
  CVE-2026-33697:
     author:
        org: CVE
     title: CoCoS attested TLS is vulnerable to relay attacks via extracted ephemeral TLS keys
     target: https://www.cve.org/CVERecord?id=CVE-2026-33697
     date: March 2026
  RA-TLS: DOI.10.1109/ACCESS.2024.3497184
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
   designers. In particular, it discusses some of the 'bottom turtle' issues. This is a work-in-progress, and the current version mainly presents an outline of the general security guidelines, baseline, or template for RATS that future versions
   will cover in more detail.

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

## Motivation
Unverified protocol designs, imprecisely stated threat model and security goals have led to high and critical severity vulnerabilities related to remote attestation.

### Concrete Motivational Example: Practical Exploits in Production Systems
{: #sec-mot-example }

The formal analysis led to three orthogonal issues:

- Formal analysis {{ID-Crisis-repo}} found **diversion** attacks when unique hardware identifier is not included in Evidence. For technical details, please see the corresponding paper {{ID-Crisis}}.

- Formal analysis {{Intra-handshake.fail-repo}} of several **production** implementations of remote attestation led to the discovery of {{CVE-2026-33697}} of **CVSS 7.5** for **relay** attacks. For technical details, please see the corresponding paper {{Intra-handshake.fail}}.

- Further formal analysis of **production** implementation of remote attestation has led to discovery of another class of attacks and will potentially lead to three CVEs (currently under *responsible* disclosure) *each* with an expected **CVSS 9.1**.

This shows the value of precise threat model and formal analysis in the design of secure protocols to find subtle vulnerabilities, which could otherwise be missed. This draft aims to provide the baseline security considerations that other drafts can simply refer to.

## Scope
To improve the situation, this draft presents general security baseline that other drafts can simply point to, or guidelines or template that other drafts can use.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

# General Hierarchy of Authentication
Authentication is a term which is often ambiguous in RATS specifications. We propose general hierarchy of one-way authentication, which can help precisely
state the intended level of authentication (in decreasing order):

* One-way injective agreement
* One-way non-injective agreement
* Aliveness

Recentness can be added to each of these levels of authentication.
Details will be added in future versions.

# Threat Modeling
This section describes "What can go wrong?"

## System Model
See Section 4 of {{Intra-handshake.fail}} as an example.

## Actors
It has both legal and technical perspective.

### Legal perspective

* Data subject is an identifiable natural person (as defined in Article 4 (1) of GDPR {{GDPR}}).
* (Data) Controller (as defined in Article 4 (7) of GDPR {{GDPR}}) manages and controls what happens with personal data of data subject.
* (Data) Processor (as defined in Article 4 (8) of GDPR {{GDPR}}) performs data processing on behalf of the data controller.

### Technical perspective

* Infrastucture Provider is a role which refers to the Processor in GDPR. An example of this role is a cloud service provider (CSP).

## Threat Model
See Section 6.1 of {{Intra-handshake.fail}} as an example.


## Typical Security Goals
See {{ID-Crisis}} as an example.

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
{{ID-Crisis-repo}} for further research and
development. Since reporting to TLS WG, these attacks have been practically
exploited in [TEE.fail](https://tee.fail/), [Wiretap.fail](https://wiretap.fail/), and [BadRAM](https://badram.eu/).

## Relay Attacks
In this attack, a network or endpoint adversary -- with access to suitable binding material -- can relay an attestation request to a genuine Attester and present the genuine Evidence as its own,
potentially resulting in impersonation of genuine Attester {{Intra-handshake.fail}}.

Note that *replay* is about *same* Attester while *relay* attack is about *different* Attesters.

# Potential Mitigations
This section describes the countermeasures and their evaluation.

To mitigate the above attacks, we propose post-handshake attestation.
We are not aware of any attacks on post-handshake attestation. Post-handshake attestation
avoids replay attacks by using a fresh attestation nonce. Moreover, considering TLS as the transport protocol, it avoids diversion and relay attacks
by binding the Evidence to the underlying TLS connection, such as using Exported Keying Material (EKM)
{{I-D.ietf-tls-rfc8446bis}}, as proposed in Section 9.2 of {{ID-Crisis}}. {{-rfc9261}} and {{-rfc9266}} provide mechanisms for such bindings. Efforts for a formal proof
of security of post-handshake attestation are ongoing.

# Security Considerations

All of this document is about security considerations.



# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

The author wishes to thank Ira McDonald and Ivan Gudymenko for insightful discussions.

# History
{:numbered="false"}

-01

* Concrete text proposal for security and privacy considerations of multi-verifiers {{I-D.deshpande-rats-multi-verifier}}

-02

* Introduction and motivation
* Defined replay and relay attacks
* Added mitigations
