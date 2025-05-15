---
title: "Applicability of Service & Infrastructure Maps (SIMAP) to Transport Networks"
abbrev: "Transport SIMAP"
category: info

docname: draft-busi-nmop-transport-simap-latest
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: ""
workgroup: "Network Management Operations"
keyword:
 - next generation
 - unicorn
 - sparkling distributed ledger
venue:
  group: "Network Management Operations"
  type: ""
  mail: "nmop@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/nmop/"
  github: "italobusi/transport-simap"
  latest: "https://italobusi.github.io/transport-simap/draft-busi-nmop-transport-simap.html"

author:
  -
    name: Italo Busi
    org: Huawei Technologies
    email: italo.busi@huawei.com
  -
    name: Haomian Zheng
    org: Huawei Technologies
    street: H1, Huawei Xiliu Beipo Village, Songshan Lake
    city: Dongguan
    region: Guangdong
    code: 523808
    country: China
    email: zhenghaomian@huawei.com

normative:

informative:


--- abstract

This document explores the applicability of the Service & Infrastructure Maps (SIMAP) concepts to transport networks and it examines the YANG data models defined by the IETF to support the requirements and use cases for SIMAP applicability to transport networks.

--- middle

# Introduction

The concept of Service & Infrastructure Maps (SIMAP) is being defined in {{!I-D.ietf-nmop-simap-concept}} together with a set of SIMP requirements and use cases.

A transport network is a server-layer network designed to provide connectivity services for a client-layer network to carry the client traffic transparently across the server-layer network resources.

A transport network typically utilizes several different transport technologies such as the Optical Transport Networks (OTN) or Wavelength Division Multiplexing (WDM).

The concept of SIMAP applies to any type of networks, including but not being limited to transport networks.

This document complements the definitions in {{!I-D.ietf-nmop-simap-concept}} providing specific requirements and use cases for SIMAP applicability to transport networks.

It also examines the YANG data models defined by the IETF to support these specific requirements and use cases at the northbound interface of an optical network controller.

## Terminology

The following terms are defined in {{!I-D.ietf-nmop-simap-concept}} and are not redefined here:

- Service & Infrastructure Maps (SIMAP)

# Overview of Key Requirements for Transport SIMAP

TODO Overview of Key Requirements for Transport SIMAP

## Resource and Bandwidth status

## Delay Measurement

## Availability

## Real-time Evaluation (Risk?)

# Use Cases

TODO Use Cases

## Planning and Service Provisioning Map

## Alarm and Incident Map

## Risk Prediction Map

# YANG Models Applicability

TODO YANG Models Applicability

## Planning and Service Provisioning

TODO Evaluate: OTN/WDM/ETH topology, Tunnel, client-signal, path computation models. Planning maybe a gap or Inventory (location) is sufficient

## Alarm and Incident

TODO Evaluate: RFC8632, Incident models

## Risk Prediction

TODO Evaluate: performance monitoring models

# Security Considerations

TODO Security

# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO Acknowledgments
