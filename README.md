# Awesome Resilient Communication [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of open protocols, applications, hardware, and resources for communication during internet shutdowns, disasters, censorship, and off-grid operation.

**Scope.** This list is about *resilient communication*: technologies that keep people able to exchange messages, files, and situational information when normal infrastructure is unavailable, degraded, or hostile. Every software entry has a working open-source implementation; resilience must be part of the architecture, not a marketing claim.

**Out of scope:**
- Cryptocurrency- and token-dependent projects, even connectivity-themed ones.
- AI tools and agent frameworks.
- Closed-source commercial products and conventional VPN services.
- Encrypted messengers that depend on centralized infrastructure (Signal, WhatsApp and similar are excellent tools, but they stop working exactly when this list becomes relevant).
- Military-only technology.

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a project.

Entries marked **Dormant** still work but have seen no meaningful development for roughly 2 years; entries marked **Experimental** are promising but not yet mature enough to rely on; dead projects live in the Graveyard section at the bottom.

**How to read this list.** "Resilient" is not one property. These six often get conflated:

- **Confidentiality** — outsiders cannot read your messages. *(encryption)*
- **Anonymity** — outsiders cannot tell who is communicating. *Encryption alone does not provide this.*
- **Metadata resistance** — outsiders cannot map who talks to whom, when, or how often. *Rarer than anonymity; most "private" tools do not have it.*
- **Censorship circumvention** — communication works despite an adversary filtering a functioning internet. *Decentralization alone does not provide this.*
- **Infrastructure independence** — communication works with no internet, cell service, or servers at all.
- **Disruption tolerance** — communication survives intermittent, high-latency, or partitioned links by storing and forwarding.

Tools in the censorship-circumvention sections need a working internet path and do nothing in a full shutdown; off-grid tools work in a full shutdown but usually offer no anonymity. No single tool covers everything.

**Inclusion is not a security endorsement.** Assume a project has had *no* independent security audit unless the entry names one. If your safety depends on a tool, evaluate your own threat model first — EFF's Surveillance Self-Defense, listed under Guides and Threat Models below, is a good starting point — and prefer audited tools with documented limitations over impressive claims.

## Contents

- [Protocols and Networking Stacks](#protocols-and-networking-stacks)
  - [Delay-Tolerant Networking](#delay-tolerant-networking)
  - [Mesh Routing and Overlay Networks](#mesh-routing-and-overlay-networks)
  - [Amateur Radio Protocols](#amateur-radio-protocols)
  - [Censorship-Resistant Transports](#censorship-resistant-transports)
  - [Anonymity Networks](#anonymity-networks)
- [Applications](#applications)
  - [Off-Grid and Local Messaging](#off-grid-and-local-messaging)
  - [Anonymous and Metadata-Resistant Messaging](#anonymous-and-metadata-resistant-messaging)
  - [Censorship Circumvention and Tool Distribution](#censorship-circumvention-and-tool-distribution)
  - [Offline Data Sync and Content Distribution](#offline-data-sync-and-content-distribution)
  - [Local-First Publishing](#local-first-publishing)
  - [Emergency Coordination](#emergency-coordination)
  - [Amateur Radio Software](#amateur-radio-software)
- [Hardware and Firmware](#hardware-and-firmware)
  - [LoRa Mesh](#lora-mesh)
  - [Mesh Router Firmware](#mesh-router-firmware)
  - [Open Hardware](#open-hardware)
- [Networks and Deployments](#networks-and-deployments)
  - [Community Networks](#community-networks)
  - [Community Cellular and Rural Connectivity](#community-cellular-and-rural-connectivity)
  - [Emergency Radio Networks](#emergency-radio-networks)
  - [Case Studies](#case-studies)
- [Measurement and Monitoring](#measurement-and-monitoring)
- [Guides and Threat Models](#guides-and-threat-models)
- [Organizations](#organizations)
- [Developer Resources](#developer-resources)
- [Graveyard](#graveyard)
- [Other Related Lists](#other-related-lists)
- [Contributors](#contributors)

## Protocols and Networking Stacks
*Protocols and building blocks for networks that tolerate disruption, partitioning, and hostile filtering.*

### Delay-Tolerant Networking
- [Bundle Protocol v7](https://datatracker.ietf.org/doc/rfc9171/) - The IETF standard (RFC 9171) for store-carry-forward networking across links with extreme delays and frequent partitions, from CubeSats to disaster areas; the foundation of the implementations below.
- [DTN7](https://dtn7.github.io/) - Rust and Go implementations of Bundle Protocol v7 with pluggable routing (epidemic, spray-and-wait), aimed at research and field deployments.
- [IBR-DTN](https://github.com/ibrdtn/ibrdtn) - Lightweight C++ bundle protocol implementation (RFC 5050) for embedded Linux and OpenWrt routers, widely cited in DTN research. **Dormant**
- [ION-DTN](https://github.com/nasa-jpl/ION-DTN) - NASA JPL's full DTN protocol suite (BPv7, LTP, CFDP), flown on space missions and usable for extreme-latency terrestrial links.
- [µD3TN](https://d3tn.gitlab.io/ud3tn/) - Lean Bundle Protocol v7 daemon in C for POSIX systems and microcontrollers, flight-tested on CubeSat missions.

### Mesh Routing and Overlay Networks
- [B.A.T.M.A.N. Advanced](https://www.open-mesh.org/projects/batman-adv/wiki) - Layer-2 mesh routing in the Linux kernel and the backbone of many community wireless networks; provides no encryption of its own.
- [Babel](https://www.irif.fr/~jch/software/babel/) - Loop-avoiding distance-vector routing protocol (RFC 8966) that behaves well on lossy wireless links; also implemented in FRRouting.
- [BMX7](https://github.com/bmx-routing/bmx7) - Mesh routing protocol with trust- and reputation-aware path selection (SEMTOR). **Dormant**
- [cjdns](https://github.com/cjdelisle/cjdns) - Encrypted IPv6 overlay and mesh network with addresses derived from public keys; runs over the internet or directly over local links. No known independent audit.
- [olsrd](https://github.com/OLSR/olsrd) - Implementation of the OLSR link-state MANET routing protocol (RFC 3626), deployed in community networks for two decades.
- [Reticulum](https://reticulum.network/) - Cryptography-first networking stack that runs over LoRa, packet radio, Wi-Fi, or IP, built for very low bandwidth and zero infrastructure, with the LXMF store-and-forward messaging layer on top. Not externally audited (self-disclosed); released under a custom non-OSI license with field-of-use restrictions.
- [Yggdrasil](https://yggdrasil-network.github.io/) - Encrypted IPv6 overlay with scalable spanning-tree routing that can also mesh over local peer discovery; self-described as experimental, no known independent audit.

### Amateur Radio Protocols
*Transmitting requires an amateur radio license, and encryption is prohibited on amateur bands in most jurisdictions — these provide availability, not confidentiality.*

- [APRS](https://www.aprs.org/) - Packet-radio protocol for positions, telemetry, and short messages over VHF, relayed node-to-node by digipeaters; works entirely off-grid, with optional internet gateways (APRS-IS).
- [AX.25](https://www.tapr.org/pdf/AX25.2.2.pdf) - The data-link protocol underlying most amateur packet radio, including APRS and Winlink RF links; implemented in the Linux kernel.
- [M17](https://m17project.org/) - Fully open digital voice and data protocol for VHF/UHF radio, using the open Codec 2 vocoder as an alternative to proprietary digital voice systems.

### Censorship-Resistant Transports
*These evade filtering on a functioning internet connection — none of them work during a full shutdown.*

- [Conjure](https://github.com/refraction-networking/conjure) - Refraction networking that lets cooperating ISPs redirect covertly tagged TLS flows to unused address space, defeating IP-based blocking; deployed in production via Psiphon.
- [Lyrebird](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/lyrebird) - The Tor Project's pluggable-transport suite (obfs4, WebTunnel, ScrambleSuit) that disguises traffic against DPI classifiers and active probing.
- [meek](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/meek) - Domain-fronting transport that hides the true destination behind large CDNs; mostly defunct since major clouds disabled fronting. **Dormant**
- [Shadowsocks](https://github.com/shadowsocks/shadowsocks-rust) - Encrypted proxy protocol designed to look like random bytes, very widely deployed for over a decade; researchers have documented active-probing and entropy-based detection of it by the Great Firewall.
- [Snowflake](https://snowflake.torproject.org/) - Routes censored users through ephemeral volunteer WebRTC proxies running in ordinary browsers, making IP blocking costly for the censor.
- [Xray-core](https://github.com/XTLS/Xray-core) - Modular proxy platform (VLESS, VMess, Trojan) that camouflages traffic as ordinary HTTPS; the most active branch of the V2Ray ecosystem. No known independent audit.

### Anonymity Networks
*Anonymity and availability are different goals: all of these require a reachable internet.*

- [I2P](https://geti2p.net/) - Decentralized garlic-routing overlay for hidden services and peer-to-peer applications; no known independent code audit, and recent academic work documents design weaknesses across its implementations.
- [Katzenpost](https://katzenpost.network/) - Mix network in the Loopix lineage providing metadata resistance without any token dependency; research-grade software with a small test network. **Experimental**
- [Tor](https://www.torproject.org/) - Onion-routing anonymity network, the base for onion services and the pluggable-transport ecosystem; repeatedly audited (most recently Cure53, 2023) with a publicly tracked vulnerability history.

## Applications
*End-user tools. Entries state what infrastructure each one actually needs.*

### Off-Grid and Local Messaging
- [Bitchat](https://github.com/permissionlesstech/bitchat) - Bluetooth LE mesh chat for iOS/macOS with no accounts or servers, widely adopted since its 2025 launch; it has had no security review, its developer warns against relying on it, and researchers reported an impersonation flaw at launch.
- [Briar](https://briarproject.org/) - Messenger that syncs over Tor when the internet works and over Bluetooth or Wi-Fi when it does not; relays only between mutual contacts, not strangers. Audited by Cure53 (2017).
- [Meshenger](https://github.com/meshenger-app/meshenger-android) - Serverless voice and video calls over the local network, usable on community mesh networks with no internet at all.
- [qaul](https://qaul.net/) - Internet-independent mesh messenger using Bluetooth LE, Wi-Fi Direct, and LAN simultaneously, with store-and-forward delivery. No known independent audit.

### Anonymous and Metadata-Resistant Messaging
- [Cwtch](https://cwtch.im/) - Metadata-resistant group messenger built on Tor onion services, with untrusted relay servers for offline delivery. No known independent audit.
- [Ricochet-Refresh](https://www.ricochetrefresh.net/) - Maintained fork of Ricochet in which every user is a Tor onion service, leaving no server-side metadata; the original was audited by NCC Group (2016), before the v3 onion migration.

### Censorship Circumvention and Tool Distribution
- [F-Droid Nearby](https://f-droid.org/en/tutorials/swap/) - Shares and installs Android apps device-to-device over local Wi-Fi and Bluetooth, letting circumvention tools spread during a total shutdown.
- [Paskoocheh](https://paskoocheh.com/) - Farsi-language distribution channel for circumvention and privacy tools, reachable via web, app, email, and Telegram so that one blocked channel is not fatal.
- [Psiphon](https://psiphon.ca/) - Multi-transport circumvention client that automatically falls back across obfuscated protocols; open client and tunnel core, centrally operated network. Audited by iSEC Partners (2014), Cure53 (2017), and 7ASecurity (2021).
- [rdsys](https://gitlab.torproject.org/tpo/anti-censorship/rdsys) - The Tor Project's bridge-distribution backend, handing out bridge addresses through independent rate-limited channels to resist enumeration by censors.

### Offline Data Sync and Content Distribution
- [Kiwix](https://kiwix.org/) - Serves compressed offline copies of Wikipedia and other reference content from a laptop or Raspberry Pi hotspot; used by schools, libraries, and disaster responders worldwide.
- [NNCP](http://www.nncpgo.org/) - Encrypted store-and-forward file and mail exchange between trusted nodes over TCP, removable media, or one-way links; a modern UUCP successor built for air gaps and sneakernets.
- [Syncthing](https://syncthing.net/) - Decentralized file synchronization that works fully on a LAN with no internet; relay and discovery servers are optional and self-hostable. Despite common claims, no independent audit is documented.

### Local-First Publishing
- [Manyverse](https://www.manyver.se/) - Client for Secure Scuttlebutt, an offline-first gossip protocol that syncs social feeds over LAN or internet; content can be encrypted, but the social graph and metadata are public by design. **Dormant**
- [ShareBoxx](https://github.com/dividebysandwich/shareboxx) - Rust reimplementation of the PirateBox concept: a standalone offline Wi-Fi box for anonymous local file sharing and chat. **Experimental**

### Emergency Coordination
- [FreeTAKServer](https://github.com/FreeTAKTeam/FreeTakServer) - Python server for the TAK (Team Awareness Kit) situational-awareness ecosystem used by civilian search-and-rescue and disaster-response teams.
- [OpenTAKServer](https://opentakserver.io/) - TAK server that runs on a Raspberry Pi on a LAN or local mesh; note that the official ATAK-CIV client is source-available under government terms, not OSI open source.
- [Sahana Eden](https://sahanafoundation.org/eden/) - Humanitarian coordination platform (missing persons, shelters, inventory, volunteers) deployed since the 2010 Haiti earthquake.
- [Ushahidi](https://www.ushahidi.com/) - Crowdsourced crisis mapping that ingests reports via SMS, web, and email — useful where only degraded channels survive.

### Amateur Radio Software
*Same caveats as the protocols above: a license is required to transmit, and content is unencrypted.*

- [Dire Wolf](https://github.com/wb2osz/direwolf) - Software TNC that turns any computer with a sound card into an AX.25 packet station, digipeater, or APRS gateway; the modem layer behind most open packet-radio tools.
- [fldigi](http://www.w1hkj.com/) - Multi-mode soundcard suite (PSK31, Olivia, RTTY, and many more) with companion forms and file-transfer tools, a staple of emergency nets for two decades.
- [FreeDATA](https://freedata.app/) - Open HF file and message transfer using Codec 2-based modems, built as the open alternative to the proprietary VARA modem.
- [FreeDV](https://freedv.org/) - Open digital voice for HF radio built on the Codec 2 low-bitrate speech codec.
- [JS8Call](http://js8call.com/) - Weak-signal HF keyboard chat derived from FT8, with store-and-forward relaying — intercontinental text messaging with no infrastructure at all.
- [Pat](https://getpat.io/) - Cross-platform Winlink email client written in Go, the standard open client for email-over-radio on Linux and macOS.
- [Xastir](https://xastir.org/) - Long-standing graphical APRS client for mapping, tracking, and messaging over RF.

## Hardware and Firmware
*Most LoRa projects below run on inexpensive ESP32/nRF52 developer boards (LilyGo, Heltec, RAK); these are commercial products whose designs are only partially open.*

### LoRa Mesh
- [MeshCore](https://github.com/meshcore-dev/MeshCore) - Lightweight LoRa mesh firmware with hybrid flood and path-based routing, a lower-overhead alternative to Meshtastic.
- [Meshtastic](https://meshtastic.org/) - The most widely used open LoRa mesh firmware and companion apps for off-grid text and location sharing; channel encryption uses shared keys with a well-known default, and key-generation flaws have received CVEs (CVE-2025-52464) — no independent audit.
- [RNode Firmware CE](https://github.com/liberatedsystems/RNode_Firmware_CE) - Community-maintained firmware that turns common LoRa boards into open long-range radio modems, primarily as the physical layer for Reticulum.

### Mesh Router Firmware
- [AREDN](https://www.arednmesh.org/) - OpenWrt-based firmware that turns commodity Wi-Fi hardware into high-throughput emergency data networks on amateur frequencies (license required).
- [Freifunk Gluon](https://gluon.readthedocs.io/) - Firmware build framework behind most German Freifunk communities' mesh nodes.
- [LibreMesh](https://libremesh.org/) - OpenWrt meta-firmware that auto-configures multi-radio community mesh networks, deployed across Latin American community networks.
- [OpenWrt](https://openwrt.org/) - The general-purpose open router firmware that AREDN, Gluon, and LibreMesh all build on.

### Open Hardware
- [LibreRouter](https://librerouter.org/) - Open-hardware multi-radio router purpose-built for community mesh networks, developed by AlterMundi; firmware ecosystem is active, hardware development is quiet.

## Networks and Deployments
*Living networks and documented real-world deployments.*

### Community Networks
- [Freifunk](https://freifunk.net/) - German federation of hundreds of local community mesh initiatives; local segments keep working even when an uplink is lost.
- [Guifi.net](https://guifi.net/) - The largest community network in the world, with tens of thousands of nodes in Spain, run as a commons since 2004.
- [NYC Mesh](https://www.nycmesh.net/) - Volunteer rooftop mesh across New York City; its Red Hook lineage stayed connected through Hurricane Sandy in 2012.

### Community Cellular and Rural Connectivity
- [Magma](https://magmacore.org/) - Linux Foundation mobile-core platform for running LTE/5G networks on commodity hardware over unreliable backhaul.
- [Rhizomatica](https://www.rhizomatica.org/) - Community-owned GSM networks in rural Mexico built on Osmocom software, operated by indigenous communities under their own spectrum concession.

### Emergency Radio Networks
- [Winlink](https://winlink.org/) - Global volunteer-run email-over-radio network used in real disaster response; a fully open path exists via Pat and ARDOP, while the official client and the fastest modems (VARA, PACTOR) are proprietary.

### Case Studies
- [Breaking Bridgefy, Again](https://www.usenix.org/conference/usenixsecurity22/presentation/albrecht) - USENIX Security 2022 paper showing the protest-marketed Bridgefy mesh app remained insecure even after adopting the Signal protocol library — a cautionary tale for any crisis-marketed messenger.
- [FireChat and the 2014 Hong Kong protests](https://globalvoices.org/2015/01/13/fact-checking-firechat-mesh-networks-coverage-hong-kong-protests/) - Fact-check showing the widely reported "mesh app powered the protests" story had almost no evidence of actual offline mesh usage.
- [NetHope's Hurricane María response](https://nethope.org/programs/emergency-preparedness-and-response/hurricane-maria-disaster-response/) - After Puerto Rico's near-total telecom collapse in 2017, recovery came mostly from conventional NGO-restored Wi-Fi and satellite links — a sober benchmark for what actually gets deployed in a catastrophe.

## Measurement and Monitoring
*You cannot route around damage you cannot see: tools that document shutdowns and censorship.*

- [Censored Planet](https://censoredplanet.org/) - Remote measurement platform that detects censorship worldwide without needing volunteers inside the censored network.
- [IODA](https://ioda.inetintel.cc.gatech.edu/) - Near-real-time detection of macroscopic internet outages and shutdowns from BGP, active probing, and darknet signals; the canonical reference for confirming shutdowns.
- [OONI Probe](https://ooni.org/) - Volunteer-run network tests documenting censorship since 2012, with open data from more than 200 countries.

## Guides and Threat Models
- [EFF Surveillance Self-Defense](https://ssd.eff.org/) - Practical security guides for protesters, journalists, and other at-risk users, maintained by the Electronic Frontier Foundation.
- [net4people/bbs](https://github.com/net4people/bbs) - Multilingual discussion forum and reading list tracking censorship-circumvention research and deployment reports.
- [Security in a Box](https://securityinabox.org/) - Digital-security guides for human rights defenders, maintained by Front Line Defenders.

## Organizations
- [Access Now Digital Security Helpline](https://www.accessnow.org/help/) - Free 24/7 security helpline for civil society, from the organization behind the #KeepItOn shutdown-tracking coalition.
- [Association for Progressive Communications](https://www.apc.org/) - Long-running network supporting community networks and connectivity rights worldwide.
- [Internet Society Community Networks](https://www.internetsociety.org/issues/community-networks/) - Grants and technical support for community-owned connectivity; co-developed the LibreRouter.
- [NetHope](https://nethope.org/) - Coalition of NGOs and technology companies that restores connectivity after disasters, including 90 Wi-Fi sites across Puerto Rico after Hurricane María.
- [Télécoms Sans Frontières](https://www.tsfi.org/) - Emergency telecom NGO deploying satellite connectivity alongside first responders since 1998.

## Developer Resources
- [p2panda](https://p2panda.org/) - Rust toolkit for building local-first, disruption-tolerant applications. **Experimental**
- [The ONE Simulator](https://github.com/akeranen/the-one) - The standard academic simulator for evaluating delay-tolerant and opportunistic routing protocols before deploying them.
- [Willow Protocol](https://willowprotocol.org/) - Sync protocol and data model for offline-first applications with fine-grained capabilities, in the Earthstar lineage. **Experimental**

## Graveyard
*Projects that shaped resilient communication but are no longer maintained. Kept for the historical record. Domains of dead projects are sometimes squatted or hijacked — where that happened, links point to archived copies.*

- [Byzantium Linux](https://github.com/Byzantium/Byzantium) - Bootable live distribution that turned any laptop into a mesh node with zero configuration. **Discontinued!**
- [Commotion Wireless](https://github.com/opentechinstitute/commotion-router) - State-Department-funded mesh firmware from the Arab Spring era; its Red Hook offshoot in Brooklyn survived Hurricane Sandy. **Discontinued!**
- [disaster.radio](https://github.com/sudomesh/disaster-radio) - Solar-powered LoRa mesh for post-disaster networking; its maintainers point to Meshtastic and Reticulum as successors. **Discontinued!**
- [FidoNet](https://en.wikipedia.org/wiki/FidoNet) - The 1980s–90s global store-and-forward BBS network and a conceptual ancestor of DTN; still run by hobbyists at a tiny scale. **Discontinued!**
- [OpenCellular](https://github.com/Telecominfraproject/OpenCellular) - Facebook's open cellular base-station platform; stewardship passed to the Telecom Infra Project and stalled. **Discontinued!**
- [PirateBox](https://github.com/PirateBox-Dev/PirateBoxScripts_Webserver) - Offline Wi-Fi box for anonymous local file sharing that seeded a whole genre; see ShareBoxx for a maintained successor. **Discontinued!**
- [Serval Project](https://github.com/servalproject/serval-dna) - Pioneering disaster mesh telephony for Android whose Rhizome store-and-forward design remains influential; unmaintained since about 2022. **Discontinued!**
- [TapDance](https://github.com/refraction-networking/tapdance) - First ISP-deployed refraction-networking design, superseded by Conjure. **Discontinued!**
- [Taylor UUCP](https://www.gnu.org/software/uucp/) - The classic Unix store-and-forward transport that carried mail and Usenet over intermittent links; NNCP is its modern successor. **Discontinued!**
- [Village Telco](https://villagetelco.org/) - The Mesh Potato combined a mesh Wi-Fi node with an analog phone port for community telephony; hardware discontinued. **Discontinued!**

## Other Related Lists
Deep dives into single technologies covered here only at the level of their resilience role:

- [alternative-internet](https://github.com/redecentralize/alternative-internet) - Broad survey of decentralization projects.
- [awesome-amateur-radio](https://github.com/mcaserta/awesome-amateur-radio) - Ham radio broadly, including emergency communications.
- [awesome-anti-censorship](https://github.com/danoctavian/awesome-anti-censorship) - Circumvention tooling and Great Firewall research.
- [awesome-decentralized-web](https://github.com/gdamdam/awesome-decentralized-web) - This list's sibling: peer-to-peer, federated, and local-first software.
- [awesome-disastertech](https://github.com/DisasterTechCrew/awesome-disastertech) - Disaster-management platforms and organizations.
- [awesome-dtn](https://github.com/dtn7/awesome-dtn) - Everything Bundle Protocol: implementations, papers, simulators.
- [awesome-hamradio](https://github.com/DD5HT/awesome-hamradio) - Software-oriented ham radio: SDR, digimodes, satellite operations.
- [awesome-local-first](https://github.com/schickling/awesome-local-first) - Offline-first software architecture: CRDTs and sync engines.
- [awesome-meshcore](https://github.com/samuk/awesome-meshcore) - The MeshCore ecosystem.
- [awesome-meshtastic](https://github.com/ShakataGaNai/awesome-meshtastic) - The Meshtastic ecosystem: hardware, apps, communities.
- [awesome-privacy](https://github.com/Lissy93/awesome-privacy) - Privacy-respecting software, including encrypted messengers.
- [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) - Self-hosted server software, including communication systems.

## Contributors

Thanks to [all contributors](https://github.com/gdamdam/awesome-resilient-communication/graphs/contributors). Contributions are welcome — see the contributing guide above.

This work is dedicated to the public domain under [CC0 1.0](LICENSE).
