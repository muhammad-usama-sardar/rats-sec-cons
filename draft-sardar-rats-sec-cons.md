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
    organization: Technical University of Dresden
    abbrev: TU Dresden
    city: Dresden
    country: Germany
    email: muhammad_usama.sardar@tu-dresden.de
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
    date: July 2026,
    target: https://github.com/muhammad-usama-sardar/intra-handshake.fail
    author:
      - ins: M. U. Sardar
      - ins: V. Dubeyko
      - ins: J-M. Jacquet
  CVE-2026-33697:
     author:
        org: CVE
     title: CoCoS attested TLS is vulnerable to relay attacks via extracted ephemeral TLS keys
     target: https://www.cve.org/CVERecord?id=CVE-2026-33697
     date: 26 March 2026
  EUVD-2026-16488:
     author:
        org: ENISA
     title: CoCoS attested TLS is vulnerable to relay attacks via extracted ephemeral TLS keys
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-16488
     date: 26 March 2026
  CVE-2026-92701:
     author:
        org: CVE
     title: Cocos AI Intra-handshake attested TLS implementation is vulnerable to session-misbinding attacks for Intel TDX verifier path
     target: https://www.cve.org/CVERecord?id=CVE-2026-92701
     date: 18 Sept 2026
  CVE-2026-92702:
     author:
        org: CVE
     title: Cocos AI Intra-handshake attested TLS implementation can accept Evidence with nil, empty, or omitted reportData in the AMD SEV-SNP path
     target: https://www.cve.org/CVERecord?id=CVE-2026-92702
     date: 18 Sept 2026
  CVE-2026-108265:
     author:
        org: CVE
     title: CVE-2026-108265
     target: https://www.cve.org/CVERecord?id=CVE-2026-108265
     date: 9 Oct 2026
  CVE-2026-108266:
     author:
        org: CVE
     title: CVE-2026-108266
     target: https://www.cve.org/CVERecord?id=CVE-2026-108266
     date: 9 Oct 2026
  CVE-2026-108267:
     author:
        org: CVE
     title: CVE-2026-108267
     target: https://www.cve.org/CVERecord?id=CVE-2026-108267
     date: 9 Oct 2026
  CVE-2026-108268:
     author:
        org: CVE
     title: CVE-2026-108268
     target: https://www.cve.org/CVERecord?id=CVE-2026-108268
     date: 9 Oct 2026
  CVE-2026-108269:
     author:
        org: CVE
     title: CVE-2026-108269
     target: https://www.cve.org/CVERecord?id=CVE-2026-108269
     date: 9 Oct 2026
  EUVD-2026-83194:
     author:
        org: ENISA
     title: EUVD-2026-83194
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-83194
     date: 18 Sept 2026
  EUVD-2026-83192:
     author:
        org: ENISA
     title: EUVD-2026-83192
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-83192
     date: 18 Sept 2026
  GHSA-Cocos-AI:
    title: "CoCoS attested TLS is vulnerable to relay attacks via extracted ephemeral TLS keys"
    date: 23 March 2026
    target: https://github.com/ultravioletrs/cocos/security/advisories/GHSA-vfgg-mvxx-mgg7
    author:
      - ins: Ultraviolet Cocos AI
  GHSA-Cocos-AI2:
    title: "Cocos AI intra-handshake attested TLS implementation is vulnerable to session-misbinding attacks for Intel TDX verifier path"
    date: 16 August 2026
    target: https://github.com/ultravioletrs/cocos/security/advisories/GHSA-4px3-wj2x-xx47
    author:
      - ins: Ultraviolet Cocos AI
  GHSA-Cocos-AI3:
    title: "Cocos AI intra-handshake attested TLS implementation can accept Evidence with nil, empty, or omitted reportData in the AMD SEV-SNP path"
    date: 16 August 2026
    target: https://github.com/ultravioletrs/cocos/security/advisories/GHSA-4r6g-mp48-j2rw
    author:
      - ins: Ultraviolet Cocos AI
  GHSA-Edgeless-Systems:
    title: "Remote attestation is susceptible to relay attacks"
    date: August 2026
    target: https://github.com/edgelesssys/contrast/security/advisories/GHSA-hjgc-jc5v-fw7h
    author:
      - ins: Edgeless Systems
  GHSA-Edgeless-Systems2:
    title: "Generated policies don't detect all image substitutions"
    date: August 2026
    target: https://github.com/edgelesssys/contrast/security/advisories/GHSA-m2qg-wrxv-h898
    author:
      - ins: Edgeless Systems
  GHSA-Edgeless-Systems3:
    title: "Existing Mesh CA key can cross manifest boundaries during Contrast peer recovery"
    date: September 2026
    target: https://github.com/edgelesssys/contrast/security/advisories/GHSA-rxcv-p3px-m3c3
    author:
      - ins: Edgeless Systems
  GHSA-Edgeless-Systems4:
    title: "Node installer leaves the host containerd configuration world-writable (0666), allowing local privilege escalation"
    date: September 2026
    target: https://github.com/edgelesssys/contrast/security/advisories/GHSA-376m-h37w-4rvq
    author:
      - ins: Edgeless Systems
  GHSA-Edgeless-Systems5:
    title: "Contrast before 1.16.0 is susceptible to remote attestation relay attacks"
    date: August 2026
    target: https://github.com/advisories/GHSA-jw33-f4wc-8736
    author:
      - ins: Edgeless Systems
  SEAT-vulnerability-report:
    title: "Relay Attacks in Intra-handshake Attestation for Confidential Agentic AI Systems"
    date: 11 Jan 2026,
    target: https://mailarchive.ietf.org/arch/msg/seat/x3eQxFjQFJLceae6l4_NgXnmsDY/
    author:
      - ins: M. U. Sardar
  GHSA-Privasys-rustls:
    title: "Privasys RA-TLS challenge mode did not bind attestation evidence to the TLS session"
    date: 3 September 2026
    target: https://github.com/Privasys/rustls/security/advisories/GHSA-j6qv-435v-r492
    author:
      - ins: Privasys
  GHSA-Privasys-go:
    title: "Privasys Go fork: RA-TLS challenge mode did not bind attestation evidence to the TLS session"
    date: 3 September 2026
    target: https://github.com/Privasys/go/security/advisories/GHSA-7jfw-53rm-phh2
    author:
      - ins: Privasys
  GHSA-Privasys-eov:
    title: "enclave-os-virtual: RA-TLS challenge certificates were not bound to the TLS session"
    date: 3 September 2026
    target: https://github.com/Privasys/enclave-os-virtual/security/advisories/GHSA-p5fp-g94g-g9m9
    author:
      - ins: Privasys
  GHSA-Privasys-eom:
    title: "enclave-os-mini: RA-TLS challenge certificates were not bound to the TLS session"
    date: 3 September 2026
    target: https://github.com/Privasys/enclave-os-mini/security/advisories/GHSA-49qm-4pj3-w2c6
    author:
      - ins: Privasys
  GHSA-Privasys-rtc:
    title: "ra-tls-clients: RA-TLS challenge verifier accepted quotes not bound to the TLS session"
    date: 3 September 2026
    target: https://github.com/Privasys/ra-tls-clients/security/advisories/GHSA-5qrc-v874-mxvx
    author:
      - ins: Privasys
  GHSA-Privasys-rtc-da:
    title: "Privasys Intra-handshake attested TLS implementation is vulnerable to Diversion Attacks"
    date: 6 September 2026
    target: https://github.com/Privasys/ra-tls-clients/security/advisories/GHSA-pj2x-5wqv-fh57
    author:
      - ins: Privasys
  GHSA-Privasys-rtc-tcu:
    title: "Privasys Intra-handshake attested TLS implementation is vulnerable to TOCTOU Attacks"
    date: 6 September 2026
    target: https://github.com/Privasys/ra-tls-clients/security/advisories/GHSA-gg8q-mfhh-wrrc
    author:
      - ins: Privasys
  GHSA-Cocos-AI4:
    title: "Cocos Intra-handshake attested TLS implementation is vulnerable to Diversion Attacks"
    date: 25 September 2026
    target: https://github.com/ultravioletrs/cocos/security/advisories/GHSA-v5m8-5wxc-vjgp
    author:
      - ins: Ultraviolet Cocos AI
  GHSA-Cocos-AI5:
    title: "Cocos AI Intra-handshake attested TLS implementation is vulnerable to TOCTOU Attacks"
    date: 25 September 2026
    target: https://github.com/ultravioletrs/cocos/security/advisories/GHSA-ghwv-vrp2-2975
    author:
      - ins: Ultraviolet Cocos AI
  ID-Crisis: DOI.10.1145/3779208.3785387
  ID-Crisis-repo:
    title: "Identity Crisis in Confidential Computing: Formal Analysis of Attested TLS"
    date: November 2025,
    target: https://github.com/CCC-Attestation/formal-spec-id-crisis
    author:
      - ins: M. U. Sardar
      - ins: M. Moustafa
      - ins: T. Aura
  refTLS: DOI.10.1109/SP.2017.26
  TLS-RA:
    title: "Separate but together: integrating remote attestation into TLS"
    date: July 2025,
    target: https://www.usenix.org/conference/atc25/presentation/weinhold
    author:
      - ins: Carsten Weinhold
      - ins: M. U. Sardar
      - ins: Ionuț Mihalcea
      - ins: Yogesh Deshpande
      - ins: Hannes Tschofenig
      - ins: Yaron Sheffer
      - ins: Thomas Fossati
      - ins: Michael Roitzsch
  CSA-eBPF:
    title: "MITRE's New Framework: Securing the eBPF Layer Your AI Depends On"
    date: 9 September 2026
    target: https://cloudsecurityalliance.org/blog/2026/09/09/mitre-s-new-framework-securing-the-ebpf-layer-your-ai-depends-on
    author:
      - ins: Cloud Security Alliance
  MITRE-Continuous-Attestation:
    title: "Framework for Continuous Remote Attestation"
    date: 16 July 2026
    target: https://www.mitre.org/news-insights/publication/framework-continuous-remote-attestation
    author:
      - ins: MITRE's Confidential Computing Layered Attestation Working Group
  EarlyAttestationBleed:
    title: "EarlyAttestationBleed: Three Critical-severity Vulnerabilities of CVSS ≥ 9.0 in Confidential Computing"
    date: 21 September 2026,
    target: https://www.researchgate.net/publication/414529199_EarlyAttestationBleed_Three_Critical-severity_Vulnerabilities_of_CVSS_90_in_Confidential_Computing
    author:
      - ins: M. U. Sardar
      - ins: Songbo Bu
  CVE-2026-100835:
     author:
        org: CVE
     title: Contrast before 1.16.0 Remote Attestation Relay Attack
     target: https://www.cve.org/CVERecord?id=CVE-2026-100835
     date: 27 Sept 2026
  EUVD-2026-87851:
     author:
        org: ENISA
     title: EUVD-2026-87851
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-87851
     date: 27 Sept 2026
  CVE-2026-100833:
     author:
        org: CVE
     title: Contrast before 1.23.1 Image Substitution via Policy Generation
     target: https://www.cve.org/CVERecord?id=CVE-2026-100833
     date: 27 Sept 2026
  EUVD-2026-87851:
     author:
        org: ENISA
     title: EUVD-2026-87851
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-87851
     date: 27 Sept 2026
  GHSA-Edgeless-Systems6:
    title: "Contrast (edgelesssys/contrast) versions 1.14.0 before 1.23.1 generate runtime policies that fail to detect all container image substitutions."
    date: 27 Sept 2026
    target: https://github.com/advisories/GHSA-MJJ6-PX65-JQ92
    author:
      - ins: Edgeless Systems
  EUVD-2026-87853:
     author:
        org: ENISA
     title: EUVD-2026-87853
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-87853
     date: 27 Sept 2026
  CVE-2026-108362:
     author:
        org: CVE
     title: CVE-2026-108362
     target: https://www.cve.org/CVERecord?id=CVE-2026-108362
     date: 12 Oct 2026
  CVE-2026-108361:
     author:
        org: CVE
     title: CVE-2026-108361
     target: https://www.cve.org/CVERecord?id=CVE-2026-108361
     date: 12 Oct 2026
  CVE-2026-112377:
     author:
        org: CVE
     title: CVE-2026-112377
     target: https://www.cve.org/CVERecord?id=CVE-2026-112377
     date: 19 Oct 2026
  EUVD-2026-95996:
     author:
        org: ENISA
     title: EUVD-2026-95996
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-95996
     date: 9 Oct 2026
  EUVD-2026-95997:
     author:
        org: ENISA
     title: EUVD-2026-95997
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-95997
     date: 9 Oct 2026
  EUVD-2026-96017:
     author:
        org: ENISA
     title: EUVD-2026-96017
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-96017
     date: 9 Oct 2026
  EUVD-2026-96018:
     author:
        org: ENISA
     title: EUVD-2026-96018
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-96018
     date: 9 Oct 2026
  EUVD-2026-96019:
     author:
        org: ENISA
     title: EUVD-2026-96019
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-96019
     date: 9 Oct 2026
  EUVD-2026-97782:
     author:
        org: ENISA
     title: EUVD-2026-97782
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-97782
     date: 12 Oct 2026
  EUVD-2026-97781:
     author:
        org: ENISA
     title: EUVD-2026-97781
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-97781
     date: 12 Oct 2026
  EUVD-2026-104535:
     author:
        org: ENISA
     title: EUVD-2026-104535
     target: https://euvd.enisa.europa.eu/enisa/EUVD-2026-104535
     date: 19 Oct 2026
  EarlyAttestationTschuess:
    title: "EarlyAttestationTschüss (EAT): 8+ Critical-Severity Vulnerabilities of CVSS 9.1 Resulting in End of Life of Early Attestation"
    date: November 2026,
    target: https://www.researchgate.net/publication/417343302_EarlyAttestationTschuss_EAT
    author:
      - ins: M. U. Sardar
      - ins: Songbo Bu
  I-D.intra-handshake-fail:

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

# Concrete CVEs

## Intra-handshake.fail
{{Intra-handshake.fail}} presents relay attacks in early attestation. From a security perspective, one of the key decision factors is the candidate binding mechanism. The formal analysis artifacts are available in {{Intra-handshake.fail-repo}} under Apache-2.0 license for reproducibility, extensibility, and further research.

- This work resulted in {{CVE-2026-33697}} of CVSS 7.5.

## ID-Crisis
A *complementary* paper {{ID-Crisis}} presents the identity crisis in pre- and intra-handshake (aka early) attestation. The formal analysis is available in {{ID-Crisis-repo}} under Apache-2.0 license for reproducibility, extensibility, and further research.

## EarlyAttestationBleed
{{EarlyAttestationBleed}} presents a formal analysis together with regression tests of the broader attestation ecosystem and discovered three critical-severity vulnerabilities in implementations of early attestation:

- Ultraviolet Cocos AI in TDX path resulting in {{CVE-2026-92701}} of CVSS 9.1.
- Ultraviolet Cocos AI in AMD SEV-SNP path resulting in {{CVE-2026-92702}} of CVSS 9.1.
- Edgeless Systems Contrast in policies resulting in {{GHSA-Edgeless-Systems2}} of CVSS 9.0-10.0 and {{CVE-2026-100833}} of CVSS v3.1 of 9.6.

### Architectural Flaws in Early Attestation

Sec. 7 of {{EarlyAttestationBleed}} presents four architectural flaws in early attestation:

- A malicious TLS client retrieves sensitive hardware-level and firmware-level information from the server’s Evidence before the server has authenticated the client.
- Early attestation can typically provide information about only boot-time Claims, since
most runtime Claims may not be available at the handshake time.
- Re-attestation requires post-handshake attestation. Early attestation thus adds unnecessary complexity.
- Early attestation results in high handshake latency, timeouts, and even failures.


## EarlyAttestationTschüss (EAT)

{{EarlyAttestationTschuess}} resulted in the following CVEs demonstrating relay and diversion attacks against early attestation implementations/deployments:

- {{CVE-2026-100835}} of CVSS 9.1 against Edgeless Systems Contrast
- {{CVE-2026-112377}} of CVSS 9.1 against CCC Attestation SIG
- {{CVE-2026-108362}} of CVSS 9.1 against Privasys
- {{CVE-2026-108265}} of CVSS 9.1 against Privasys
- {{CVE-2026-108266}} of CVSS 9.1 against Privasys
- {{CVE-2026-108267}} of CVSS 9.1 against Privasys
- {{CVE-2026-108268}} of CVSS 9.1 against Privasys
- {{CVE-2026-108269}} of CVSS 9.1 against Privasys

## More details

Further examples of CVEs are in {{I-D.intra-handshake-fail}}.

# Potential Mitigations
This section describes the countermeasures and their evaluation.

To mitigate the above attacks, we propose post-handshake attestation.
Post-handshake attestation
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

The authors wish to thank Ira McDonald and Ivan Gudymenko for insightful discussions.

# History
{:numbered="false"}

-01

* Concrete text proposal for security and privacy considerations of multi-verifiers

-02

* Introduction and motivation
* Defined replay and relay attacks
* Added mitigations

-07

* Added CVEs

-08

* Explained architectural flaws
