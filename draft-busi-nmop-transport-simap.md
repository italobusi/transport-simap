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

The following terms are defined in {{!rfc9543}} and are not redefined here:

- Service Level Agreement (SLA)

> Editors' Note: should we differentiate between SLA, SLO, SLE and SLI within this I-D?

# Overview of Key Requirements for Transport SIMAP

TODO Overview of Key Requirements for Transport SIMAP

## Resource and Bandwidth status

## Delay Measurement

## Availability

## Real-time Evaluation (Risk?)

# Use Cases

## Service Provisioning

A transport network provides connectivity services to carry the client traffic transparently.

In order to allow monetization of the transport network connectivity services, transport networks are evolving to support connectivity services with differentiated SLAs.

Transport networks can support connectivity services with different requirements in terms of bandwidth, delay and availability, or any combination of them. For examples, some services may have different bandwidth requirements (e.g., 10G, 100G) or different delay requirements or different availability requirements. Other services can have both bandwidth and delay requirements or both delay and availability requirements.

An optical network controller is able to receive connectivity service requests with constraints in terms of bandwidth or delay or availability or any combination of them.

A transport network typically utilizes several different transport technologies such as the Optical Transport Networks (OTN) or Wavelength Division Multiplexing (WDM). Therefore the request to setup a new connectivity service would trigger multi-layer path computation and setup e.g. to determine whether:

1. an OTN tunnel already exists within the transport network to carry the new requested connectivity service while meeting the requested bandwidth, delay and availability requirements: in this case the optical network controller just configures the connectivity service on the two devices at the edge of the selected OTN tunnel;

1. a new OTN tunnel needs to be setup with the transport network and whether the path of this new OTN tunnel:

   {: type="a"}

   1. can re-use existing links or server-layer WDM tunnels: in this case the optical network controller starts the OTN tunnel setup procedure (e.g., through GMPLS signalling) and then configures the connectivity service on the two devices at the edge of the just set up OTN tunnel;

   1. requires the setup of one ore more new WDM tunnels within the transport network: in this case the optical network controller:

      {: type="i"}

      1. starts the WDM tunnel setup procedure (e.g., through GMPLS signalling) for all the new WDM tunnels which need to be setup;

      1. start the OTN tunnel setup procedure (e.g., through GMPLS signalling);

      1. configures the connectivity service on the two devices at the edge of the just set up OTN tunnel.

The WDM path computation performed by the optical controller needs to have the complete visibility of all the resources within the WDM layer in order to compute the optimal feasible optical path, taking into account the characteristics (e.g., optical impairments) of the ROADM nodes, the capabilities of the transceivers. It also needs to know the existing OTSi signals within the optical network to determine the optical impairment impact of the existing OTSi signals on the optical feasibility of a new OTSi signal and vice versa, i.e., the impact of the new OTSi on the existing OTSi signals: see {{Section 2.3.1 of ?I-D.ietf-ccamp-optical-impairment-topology-yang}}.

In order to provide the requested level of availability, optical path computation at any layer (e.g., OTN or WDM) shall be able to compute SRLG disjoint paths in order to avoid that a single failure would impact also the backup path.

Manual configuration of SRLG is error-prone because of human errors and the lack of complete information on how the physical infrastructure is built (e.g., where the fibers are physically lay down).

The optical controller can implement advanced algorithms to automatically detect co-cabling (i.e., fibers which are assembled within the same cable) as well as co-trenching (i.e., cables which are lay down on the same trench). These automatic mechanisms can reduce the errors in provisioning SRLG information thus improving the provisioning of services with guaranteed availability.

The mechanisms used by the optical controller to detect co-cabling and co-trenching are implementation specific and outside the scope of standardization. The Transport SIMAP reports the output of these mechanisms thought standardized network topology and inventory models.

## Alarm and Incident

Alarm and Incident are defined in {{?I-D.ietf-nmop-terminology}}.

In transport network an incident can cause alarms or state down on multiple tunnels and services. For example:
- a fiber break will cause all the WDM tunnels routed through this fiber to go down;
- a WDM tunnel failure will cause all the OTN tunnels routed through it to go down;
- an OTN tunnel failure will cause all the services (e.g., CBR or Ethernet services) supported by it to go down.

Note that, while usually an OTN tunnel can carry only one service, there are some cases where multiple services are multiplexed over the same OTN tunnel.

When an accident occurs in the transport network, Transport SIMAP is able to report the root alarm/condition (e.g., the fiber break) that is associated with the incident and all the consequent alarms/conditions (e.g., WDM tunnels, OTN tunnels and services being down).

This will allow the operator to know which tunnels and services are impacted by the incident and which is the root cause to be resolved in order to bring them up again.

By supporting the co-cabling and co-trenching mechanisms, the Transport SIMAP can also provide a deeper analysis of the incident. For example, if a cable breaks, Transport SIMAP can report the cable break as the root cause for the consequent alarms reporting fiber breaks.

{{?I-D.ietf-nmop-network-incident-yang}} provide also more details about incident management.

## Risk Prediction

> Related with protection and restoration. Current approach is based on the monitoring of the status of the connection (SF or SD) triggering re-routing. SF is mainly related to loss of continuity. What about latency degradation?

> Provide more enhanced SD definitions (latency)

When a connectivity service with availability requirements is requested, the optical controller can decide to configure some resiliency (e.g., protection or restoration) mechanisms within the network to recover the service traffic in case a failure or a degradation occur.

Transport SIMAP reports the configuration of the mechanism as well as its status.

In particular, after a failure or a degradation occurs, the service resiliency mechanism may be in a state which will not allow the transport network to recover any additional failure (for example, the 1+1 protection mechanism is not able to recover from the failure of the secondary path after the primary path has failed and the traffic has switched to the secondary path).

Based on the status of the resiliency mechanism reported by Transport SIMAP, the customer may request to reconfigure the service availability requirements (e.g., from 1+1 to always-1+1) or do nothing.

> More discussion to be done based on the availability monetization description

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
