---
title: Expanding the IPv6 Lab Use Space
abbrev: Expanding the IPv6 Lab Use Space
docname: draft-horley-v6ops-lab-01
cat: std
ipr: trust200902
area: Int
wg: V6OPS
kw: Internet-Draft


author:
      -
        ins: N. Buraglio
        name: Nick Buraglio
        org: Energy Sciences Network
        email: buraglio@forwardingplane.net
      -
        ins: C. Cummings
        name: Chris Cummings
        org: Energy Sciences Network
        email: chriscummings@es.net
      -
        ins: Kevin Myers
        org: IP ArchiTechs
        email: kevin.myers@iparchitechs.com
      -
       ins: Russ White
       org: Juniper Networks
       email: russ@riw.us
      -
        ins: E. Horley
        name: Ed Horley
        org: Hexabuild
        email: ed@hexabuild.io
      -
        ins: T. Coffeen
        name: Tom Coffeen
        org: Hexabuild
        email: tom@hexabuild.io
      -
        ins: S. Hogg
        name: Scott Hogg
        org: Hexabuild
        email: scott@hexabuild.io

normative:
  RFC2119:
  RFC8200:   

informative:
  RFC6724:
  RFC1918:
  RFC3484:
  RFC3513:    
  RFC3515:
  RFC4048:
  RFC4193:
  RFC7078:
  RFC7526:
  RFC4193:
  RFC4291:
  RFC4548:
  RFC5180:
  RFC6890:
 
  

--- abstract

To reduce the likelihood of addressing conflicts and confusion between lab deployments and non-lab (i.e., production) deployments, an IPv6 unicast address prefix is reserved for use in lab, proof-of-concept, and validation networks as well as for any similar use case. This document describes the use of the IPv6 address prefix 0200::/7 as a prefix reserved for this purpose (repurposing the deprecated OSI NSAP-mapped prefix).

--- middle

# Introduction

The address architecture for IPv6 {{RFC4291}} does not explicitly define any prefixes allocated exclusively for lab use, nor is such address space allocated in {{RFC6890}} or in {{RFC8200}}. While lab deployments could potentially use IPv6 address prefixes typically assigned and configured in non-lab network, the use of such addressing in lab environments may create addressing conflicts and operational confusion. For instance, designing labs utilizing ULA fc00::/7 {{RFC4193}} is problematic due to the random global ID requirement preventing hierarchical network prefix design possibilities. Further, default address selection behavior {{RFC6724}} by end nodes may result in a de-preferencing of such addresses and prevent lab deployments from accurately modeling their desired non-lab equivalents.
To resolve these problems involved in building large-scale lab networks, and pre-staging, or automating large-scale networks for deployment, this document allocates the IPv6 address prefix 0200::/7 for these purposes.
The goal is to allow organization to share working lab configuration files (with little or no need of modification) to be deployed in a third party lab environment like, public and private clouds, virtualization or hosting environments,
and in other networks like Service Providers, Enterprise, Government, IoT, and Energy,
all with the knowledge that the lab GUA address space will perform the same as any GUA but with the added knowledge that filtering will be used to protect accidental leaks to the Internet.
The following criteria is for selecting the lab prefix:
The precedence for the lab prefix should no be lower than the GUA prefix as defined in {{RFC6724}} (unlike ULA). Reduce the operational impacts to IANA and the RIR's in selecting lab prefix space.

# Terminology

{::boilerplate bcp14-tagged}

# Assignment of address space for use in large-scale lab and prototyping environments 

The prefix reserved for large scale lab and testing purposes is 0200::/7.

## Operational Implications

This space SHOULD NOT be employed for addressing use cases which are already defined in other RFCs, such as addresses set apart for documentation, testing, etc.
Enterprise and large-scale networks have some specific criteria around building and validating prior to deployment. The issues with ULA for infrastructure modeling, lab creation, configuration and behavior testing at the host level are notably impactful in large enterprises as well as continental and global scale networks. This is primarily, but not exclusively, due to the increased focus on large-scale hosts, servers, and application testing. Additionally, it is likely that both GUA and ULA may co-exist or are planned to co-exist, and reconfiguring lab hosts, network elements, operational technology systems, and IoT hardware isn't practical or desirable due to inconsistent results for host preference due to {{RFC6724}} behavior.
Most large-scale enterprises strive to build lab, dev, and QA environments that reflect production as accurately as possible. This is a fairly straightforward way to avoid disparity between production and non-production. Enterprise environments are an area that need increased IPv6 adoption. In an effort to enable a more approachable mechanism to model a global scale network,  and to avoid the pitfalls of ULA de-preferenced host behavior or mis-use (i.e. address space squatting) on other IPv6 space, a specific IPv6 lab prefix is being assigned.
Because this address prefix has previously been used for the OSI NSAP-mapped prefix set in {{RFC4048}} and {{RFC4548}}, and deprecated, this address prefix is already limited in its usability. In addition, the address prefix was returned to IANA and is available to be marked for lab or other purposes.
This assignment implies that IPv6 network operators SHOULD add this address prefix to the list of non-routable IPv6 address space, and if packet filters are deployed, then this address prefix SHOULD be added to packet filters. This is not a local-use address prefix so these filters may be used in both local and public contexts.


# Acknowledgements 

The authors would like to acknowledge the valuable input and contributions of the v6ops WG. The authors further acknowledge the work of Bob Hinden and Stephen Deering, in authoring the protocol standard and the addressing architecture for IPv6.

# Security Considerations

The addresses assigned for lab and staging use SHOULD be filtered as noted above.
Setting aside address space for lab and staging use, and adding this address space to common filters to prevent destinations in this space from being routed in production networks (including the global Internet) improves security by preventing the leakage of prefixes used for testing into production environments. As such, setting aside this space improves the overall security posture of the Internet.

# IANA Considerations

IANA to allocate and record the reservation of the IPv6 global unicast address prefix 0200::/7 as a lab-only prefix in the IPv6 address registry. No end party is to be assigned this address.

# Appendix A. 

--- back
