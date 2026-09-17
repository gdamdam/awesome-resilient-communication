# Awesome Resilient Communication [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

A curated list of open protocols, applications, hardware, and resources for communication during internet shutdowns, disasters, censorship, and off-grid operation.

**Scope.** Tools that keep people exchanging messages, files, and situational information when normal infrastructure is down, degraded, or hostile. Every software entry has a working open-source implementation. A few flagged exceptions are source-available under non-OSI terms. Resilience must be in the architecture, not in the marketing.

**Out of scope:**
- Cryptocurrency- and token-dependent projects.
- AI tools and agent frameworks.
- Closed-source products and conventional VPN services.
- Encrypted messengers that depend on central servers. Signal and WhatsApp are excellent, but they stop working exactly when you need this list.
- Military-only technology.

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting a project.

**Dormant** entries still work but have had no real development for about 2 years. **Experimental** entries are promising but not yet ready to rely on. Dead projects are in the Graveyard at the bottom.

**How to read this list.** "Resilient" means six different things that often get mixed up:

- **Confidentiality**: outsiders cannot read your messages. Encryption gives you this.
- **Anonymity**: outsiders cannot tell who is talking. Encryption alone does not.
- **Metadata resistance**: outsiders cannot map who talks to whom, when, or how often. Most "private" tools lack it.
- **Censorship circumvention**: communication works on a filtered internet. Decentralization alone does not give you this.
- **Infrastructure independence**: communication works with no internet, cell service, or servers.
- **Disruption tolerance**: communication survives intermittent or broken links by storing and forwarding.

No single tool covers all six. The first four matter when the internet works but is watched or filtered; the last two when connectivity itself has failed.

**Inclusion is not a security endorsement.**

- Assume no independent audit unless the entry names one.
- If your safety depends on a tool, start from your own threat model. EFF's Surveillance Self-Defense, under Guides and Threat Models below, is a good place to begin.
- Prefer audited tools with known limitations over impressive claims.
- Audit citations, encryption defaults, and metadata notes were last checked in September 2026. Treat them as snapshots and check upstream.

**How this list is maintained.** Inclusion, exclusion, and the criteria above are decided by a human maintainer, me, by hand. AI tooling helps draft entry text and cross-check licenses, audit citations, and project status. Every claim is verified against the project's own documentation before it lands.

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
- [Resilience at a Glance](#resilience-at-a-glance)
- [Hardware and Firmware](#hardware-and-firmware)
  - [LoRa Mesh](#lora-mesh)
  - [Mesh Router Firmware](#mesh-router-firmware)
  - [Open Hardware](#open-hardware)
- [Networks and Deployments](#networks-and-deployments)
  - [Community Networks](#community-networks)
  - [Community Cellular and Rural Connectivity](#community-cellular-and-rural-connectivity)
  - [Emergency Radio Networks](#emergency-radio-networks)
  - [Legacy but Operational Networks](#legacy-but-operational-networks)
  - [Case Studies](#case-studies)
- [Measurement and Monitoring](#measurement-and-monitoring)
- [Prepare Before You Need It](#prepare-before-you-need-it)
- [Guides and Threat Models](#guides-and-threat-models)
- [Organizations](#organizations)
- [Developer Resources](#developer-resources)
- [Graveyard](#graveyard)
- [Other Related Lists](#other-related-lists)
- [Contributors](#contributors)

## Protocols and Networking Stacks
*Building blocks for networks that keep working when links break, partition, or get filtered.*

### Delay-Tolerant Networking
- [Bundle Protocol v7](https://datatracker.ietf.org/doc/rfc9171/) - The IETF standard (RFC 9171) for store-carry-forward networking over links with long delays and frequent partitions. Used from CubeSats to disaster areas. The implementations below all build on it.
- [DTN7](https://dtn7.github.io/) - Bundle Protocol v7 in Rust and Go, with pluggable routing (epidemic, spray-and-wait). Aimed at research and field deployments.
- [IBR-DTN](https://github.com/ibrdtn/ibrdtn) - Small C++ bundle protocol implementation (RFC 5050) for embedded Linux and OpenWrt routers. Widely cited in DTN research. **Dormant**
- [ION-DTN](https://github.com/nasa-jpl/ION-DTN) - NASA JPL's full DTN suite (BPv7, LTP, CFDP). Flown on space missions, and usable for terrestrial links with extreme latency.
- [µD3TN](https://d3tn.gitlab.io/ud3tn/) - Small Bundle Protocol v7 daemon in C for POSIX systems and microcontrollers. Flight-tested on CubeSats.

### Mesh Routing and Overlay Networks
- [B.A.T.M.A.N. Advanced](https://www.open-mesh.org/projects/batman-adv/wiki) - Layer-2 mesh routing in the Linux kernel. The backbone of many community wireless networks. No encryption of its own.
- [Babel](https://www.irif.fr/~jch/software/babel/) - Distance-vector routing protocol (RFC 8966) that avoids loops and behaves well on lossy wireless links. Also implemented in FRRouting.
- [BMX7](https://github.com/bmx-routing/bmx7) - Mesh routing with trust- and reputation-aware path selection (SEMTOR). **Dormant**
- [cjdns](https://github.com/cjdelisle/cjdns) - Encrypted IPv6 overlay and mesh with addresses derived from public keys. Runs over the internet or directly over local links.
- [olsrd](https://github.com/OLSR/olsrd) - OLSR link-state MANET routing (RFC 3626). Deployed in community networks for two decades.
- [Reticulum](https://reticulum.network/) - Cryptography-first networking stack that runs over LoRa, packet radio, Wi-Fi, or IP. Built for very low bandwidth and zero infrastructure, with LXMF store-and-forward messaging on top. Custom non-OSI license with field-of-use restrictions.
- [Yggdrasil](https://yggdrasil-network.github.io/) - Encrypted IPv6 overlay with spanning-tree routing that can also mesh over local peer discovery. The project calls itself experimental.

### Amateur Radio Protocols
*You need an amateur radio license to transmit, and most jurisdictions forbid encryption on amateur bands. These give you availability, not confidentiality.*

- [APRS](https://www.aprs.org/) - Packet radio for positions, telemetry, and short messages over VHF, relayed node to node by digipeaters. Works entirely off-grid. Internet gateways (APRS-IS) are optional.
- [AX.25](https://en.wikipedia.org/wiki/AX.25) - The data-link protocol under most amateur packet radio, including APRS and Winlink RF links. Implemented in the Linux kernel.
- [M17](https://m17project.org/) - Open digital voice and data protocol for VHF/UHF, using the open Codec 2 vocoder instead of proprietary digital voice systems.

### Censorship-Resistant Transports
*These get around filtering on an internet that still works. None of them work in a full shutdown.*

- [Conjure](https://github.com/refraction-networking/conjure) - Refraction networking: cooperating ISPs redirect covertly tagged TLS flows to unused address space, so IP blocking fails. In production via Psiphon.
- [Lyrebird](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/lyrebird) - The Tor Project's pluggable transports (obfs4, WebTunnel, ScrambleSuit). Disguises traffic against DPI classifiers and active probing.
- [meek](https://gitlab.torproject.org/tpo/anti-censorship/pluggable-transports/meek) - Domain fronting: hides the real destination behind a large CDN. Mostly defunct since the major clouds disabled fronting. **Dormant**
- [Shadowsocks](https://github.com/shadowsocks/shadowsocks-rust) - Encrypted proxy protocol designed to look like random bytes. Very widely deployed for over a decade. Researchers have documented the Great Firewall detecting it through active probing and entropy analysis.
- [Snowflake](https://snowflake.torproject.org/) - Routes censored users through short-lived volunteer WebRTC proxies running in ordinary browsers. Blocking by IP gets expensive for the censor.
- [Xray-core](https://github.com/XTLS/Xray-core) - Modular proxy platform (VLESS, VMess, Trojan) that makes traffic look like ordinary HTTPS. The most active branch of the V2Ray ecosystem.

### Anonymity Networks
*Anonymity and availability are different goals. All of these need a reachable internet.*

- [I2P](https://i2p.net/) - Decentralized garlic-routing overlay for hidden services and peer-to-peer apps. Recent academic work documents design weaknesses across its implementations.
- [Katzenpost](https://katzenpost.network/) - Mix network in the Loopix lineage, built for metadata resistance and free of any token dependency. Research-grade software with a small test network. **Experimental**
- [Tor](https://www.torproject.org/) - Onion-routing anonymity network, and the base for onion services and the pluggable-transport ecosystem. Audited repeatedly (most recently Cure53, 2023), with a public vulnerability history.

## Applications
*End-user tools. Each entry says what infrastructure the tool actually needs.*

### Off-Grid and Local Messaging
- [Bitchat](https://github.com/permissionlesstech/bitchat) - Bluetooth LE mesh chat for iOS and macOS. No accounts, no servers. Widely adopted since its 2025 launch. Its own developer warns against relying on it for security, and researchers reported an impersonation flaw at launch.
- [Briar](https://briarproject.org/) - Messenger that syncs over Tor when the internet works and over Bluetooth or Wi-Fi when it does not. Relays only between mutual contacts, not strangers. Audited by Cure53 (2017).
- [Columba](https://github.com/torlando-tech/columba) - Android messaging and voice client for Reticulum (LXMF/LXST). Connects over Bluetooth LE, Wi-Fi/TCP, or LoRa via RNode radios, and can bridge those interfaces so a local Bluetooth mesh reaches across a LAN or the internet. MPL-2.0, Android only.
- [Meshenger](https://github.com/meshenger-app/meshenger-android) - Voice and video calls over the local network with no server. Works on community mesh networks with no internet at all.
- [Meshing Around](https://github.com/SpudGunMan/meshing-around) - Python bot that turns a Meshtastic node into a BBS: store-and-forward mail, scheduled broadcasts, emergency-keyword alerts, mesh health tests, and lookups in a local Kiwix copy. Bridges up to nine meshes from one Raspberry Pi. The weather, email/SMS, and LLM features need internet or a local server, and Meshtastic's channel-encryption caveats apply.
- [qaul](https://qaul.net/) - Mesh messenger that uses Bluetooth LE, Wi-Fi Direct, and LAN at the same time, with store-and-forward delivery. No internet needed.

### Anonymous and Metadata-Resistant Messaging
- [Cwtch](https://cwtch.im/) - Metadata-resistant group messenger on Tor onion services. Untrusted relay servers handle offline delivery.
- [Ricochet-Refresh](https://www.ricochetrefresh.net/) - Maintained fork of Ricochet. Every user is a Tor onion service, so there is no server-side metadata. The original was audited by NCC Group (2016), before the v3 onion migration.

### Censorship Circumvention and Tool Distribution
- [F-Droid Nearby](https://f-droid.org/en/tutorials/swap/) - Shares and installs Android apps device to device over local Wi-Fi and Bluetooth. This is how circumvention tools spread during a total shutdown.
- [Paskoocheh](https://paskoocheh.com/) - Farsi-language distribution channel for circumvention and privacy tools. Reachable by web, app, email, and Telegram, so blocking one channel does not kill it.
- [Psiphon](https://psiphon.ca/) - Circumvention client that falls back across several obfuscated transports on its own. Open client and tunnel core, centrally operated network. Audited by iSEC Partners (2014), Cure53 (2017), and 7ASecurity (2021).
- [rdsys](https://gitlab.torproject.org/tpo/anti-censorship/rdsys) - The Tor Project's bridge-distribution backend. Hands out bridge addresses through independent rate-limited channels so censors cannot enumerate them.

### Offline Data Sync and Content Distribution
- [Kiwix](https://kiwix.org/) - Serves compressed offline copies of Wikipedia and other reference content from a laptop or Raspberry Pi hotspot. Used by schools, libraries, and disaster responders.
- [NNCP](http://www.nncpgo.org/) - Encrypted store-and-forward file and mail exchange between trusted nodes over TCP, removable media, or one-way links. A modern UUCP built for air gaps and sneakernets.
- [Syncthing](https://syncthing.net/) - Decentralized file sync that works fully on a LAN with no internet. Relay and discovery servers are optional and can be self-hosted.

### Local-First Publishing
- [Manyverse](https://www.manyver.se/) - Client for Secure Scuttlebutt, an offline-first gossip protocol that syncs social feeds over LAN or internet. Content can be encrypted. The social graph and metadata are public by design.
- [ShareBoxx](https://github.com/dividebysandwich/shareboxx) - Rust reimplementation of PirateBox: a standalone offline Wi-Fi box for anonymous local file sharing and chat. **Experimental**

### Emergency Coordination
- [FreeTAKServer](https://github.com/FreeTAKTeam/FreeTakServer) - Python server for TAK (Team Awareness Kit), the situational-awareness ecosystem used by civilian search-and-rescue and disaster-response teams.
- [OpenTAKServer](https://opentakserver.io/) - TAK server that runs on a Raspberry Pi on a LAN or local mesh. Note that the official ATAK-CIV client is source-available under government terms, not OSI open source.
- [Sahana Eden](https://sahanafoundation.org/eden/) - Humanitarian coordination platform (missing persons, shelters, inventory, volunteers). Deployed since the 2010 Haiti earthquake.
- [Ushahidi](https://www.ushahidi.com/) - Crowdsourced crisis mapping that takes reports by SMS, web, and email. Useful where only degraded channels survive.

### Amateur Radio Software
*Same caveats as the protocols above: you need a license to transmit, and nothing is encrypted.*

- [Dire Wolf](https://github.com/wb2osz/direwolf) - Software TNC that turns any computer with a sound card into an AX.25 packet station, digipeater, or APRS gateway. The modem layer behind most open packet-radio tools.
- [fldigi](https://www.w1hkj.org/) - Multi-mode soundcard suite (PSK31, Olivia, RTTY, and many more) with companion forms and file-transfer tools. In use on emergency nets for two decades.
- [FreeDATA](https://freedata.app/) - Open HF file and message transfer using Codec 2-based modems. Built as the open alternative to the proprietary VARA modem.
- [FreeDV](https://freedv.org/) - Open digital voice for HF radio, built on the Codec 2 low-bitrate speech codec.
- [JS8Call](http://js8call.com/) - Weak-signal HF keyboard chat derived from FT8, with store-and-forward relaying. Text across continents with no infrastructure.
- [Pat](https://getpat.io/) - Winlink email client written in Go. The standard open client for email over radio on Linux and macOS.
- [Xastir](https://github.com/Xastir/Xastir) - Long-running graphical APRS client for mapping, tracking, and messaging over RF.

## Resilience at a Glance
|System          |Confidentiality|Anonymity|Metadata resistance|Censorship circumvention|Infrastructure independence|Disruption tolerance|
|----------------|---------------|---------|-------------------|------------------------|---------------------------|--------------------|
|Psiphon         |N/A            |✗        |✗                  |✓                       |✗                          |N/A                 |
|Ricochet Refresh|✓              |✓        |✓                  |◐                       |✗                          |✗                   |
|Cwtch           |✓              |✓        |✓                  |◐                       |✗                          |◐                   |
|Briar           |✓              |✓        |✓                  |✓                       |✓                          |◐                   |
|Bitchat         |◐              |◐        |✗                  |✗                       |✓                          |✓                   |
|qaul            |✓              |✗        |✗                  |✗                       |✓                          |✓                   |
|Meshtastic      |◐              |✗        |✗                  |✗                       |✓                          |◐                   |
|Reticulum / LXMF|✓              |◐        |◐                  |✗                       |✓                          |✓                   |
|NNCP            |✓              |✗        |◐                  |✗                       |✓                          |✓                   |
|Syncthing       |✓              |✗        |✗                  |✗                       |◐                          |◐                   |
|Winlink         |✗              |✗        |✗                  |✗                       |◐                          |✓                   |

✓ designed to provide it · ◐ partial, conditional, or configuration-dependent · ✗ generally not provided · N/A not meaningfully applicable

## Hardware and Firmware
*Most LoRa projects below run on cheap ESP32 and nRF52 developer boards (LilyGo, Heltec, RAK). Those are commercial products, and their designs are only partly open.*

### LoRa Mesh
- [MeshCore](https://github.com/meshcore-dev/MeshCore) - Lightweight LoRa mesh firmware with hybrid flood and path-based routing. Lower overhead than Meshtastic.
- [Meshtastic](https://meshtastic.org/) - The most widely used open LoRa mesh firmware, with companion apps for off-grid text and location sharing. Channel encryption defaults to a well-known shared key. Private channels with custom keys are supported, and firmware 2.5 added public-key encryption for direct messages. Key-generation flaws have received CVEs (CVE-2025-52464).
- [RNode Firmware CE](https://github.com/liberatedsystems/RNode_Firmware_CE) - Community-maintained firmware that turns common LoRa boards into open long-range radio modems. Mainly the physical layer for Reticulum.

### Mesh Router Firmware
- [AREDN](https://www.arednmesh.org/) - OpenWrt-based firmware that turns commodity Wi-Fi hardware into high-throughput emergency data networks on amateur frequencies. License required.
- [Freifunk Gluon](https://gluon.readthedocs.io/) - Firmware build framework behind most German Freifunk mesh nodes.
- [LibreMesh](https://libremesh.org/) - OpenWrt meta-firmware that auto-configures multi-radio community mesh networks. Deployed across community networks in Latin America.
- [OpenWrt](https://openwrt.org/) - The general-purpose open router firmware that AREDN, Gluon, and LibreMesh all build on.

### Open Hardware
- [LibreRouter](https://gitlab.com/librerouter) - Open-hardware multi-radio router built for community mesh networks, by AlterMundi. The firmware side is active. Hardware development is quiet.

## Networks and Deployments
*Networks that exist today, and deployments with a documented record.*

### Community Networks
- [Freifunk](https://freifunk.net/) - German federation of hundreds of local community mesh initiatives. Local segments keep working when the uplink is lost.
- [Guifi.net](https://guifi.net/) - The largest community network in the world: tens of thousands of nodes in Spain, run as a commons since 2004.
- [NYC Mesh](https://www.nycmesh.net/) - Volunteer rooftop mesh across New York City. Its Red Hook lineage stayed connected through Hurricane Sandy in 2012.

### Community Cellular and Rural Connectivity
- [Magma](https://magmacore.org/) - Linux Foundation mobile-core platform for running LTE and 5G networks on commodity hardware over unreliable backhaul.
- [Rhizomatica](https://www.rhizomatica.org/) - Community-owned GSM networks in rural Mexico, built on Osmocom software and run by indigenous communities under their own spectrum concession.

### Emergency Radio Networks
- [Winlink](https://winlink.org/) - Global volunteer-run email-over-radio network used in real disaster response. A fully open path exists through Pat and ARDOP. The official client and the fastest modems (VARA, PACTOR) are proprietary.

### Legacy but Operational Networks
- [FidoNet](https://www.fidonet.org/) - The global store-and-forward BBS network of the 1980s and 90s, and an ancestor of DTN ([history](https://en.wikipedia.org/wiki/FidoNet)). Long past its peak but still running, with a weekly nodelist and around a thousand active nodes.

### Case Studies
- [Breaking Bridgefy, Again](https://www.usenix.org/conference/usenixsecurity22/presentation/albrecht) - USENIX Security 2022 paper. The protest-marketed Bridgefy mesh app stayed insecure even after adopting the Signal protocol library. Worth reading before trusting any messenger marketed for crises.
- [FireChat and the 2014 Hong Kong protests](https://globalvoices.org/2015/01/13/fact-checking-firechat-mesh-networks-coverage-hong-kong-protests/) - Fact-check of the "mesh app powered the protests" story. Almost no evidence of actual offline mesh use.
- [NetHope's Hurricane María response](https://nethope.org/programs/emergency-preparedness-and-response/hurricane-maria-disaster-response/) - After Puerto Rico's near-total telecom collapse in 2017, most recovery came from NGO-restored Wi-Fi and satellite links, not mesh. A realistic picture of what actually gets deployed in a catastrophe.

## Measurement and Monitoring
*You cannot route around damage you cannot see. These document shutdowns and censorship.*

- [Censored Planet](https://censoredplanet.org/) - Remote measurement platform that detects censorship worldwide without volunteers inside the censored network.
- [IODA](https://ioda.inetintel.cc.gatech.edu/) - Near-real-time detection of large internet outages and shutdowns from BGP, active probing, and darknet signals. The usual reference for confirming a shutdown.
- [OONI Probe](https://ooni.org/) - Volunteer-run network tests documenting censorship since 2012. Open data from more than 200 countries.

## Prepare Before You Need It
Nearly everything here shares one failure mode: it only works if it was set up before the outage. App stores are unreachable during a shutdown. F-Droid Nearby can spread apps device-to-device afterwards, but only from someone who downloaded them in time. The same applies beyond installation:

- Contacts and keys: Briar contacts must be exchanged while a channel still exists, and its Mailbox needs a spare device set up in advance.
- Circumvention channels: Tor bridges and Psiphon builds are easiest to get before censorship tightens. That is why rdsys distributes bridges through several independent channels.
- Hardware: LoRa radios must be bought, flashed, and key-exchanged ahead of time. A first field test during a disaster is a bad field test.
- Skills and licenses: an amateur radio license takes weeks, and the skill that makes emergency nets work comes from joining them routinely.
- Reference material: offline maps, medical guides, and Wikipedia dumps are tens of gigabytes and a separate discipline, covered by the sibling list awesome-offline-knowledge under Other Related Lists below.

A reasonable minimum: pick the failure modes that apply to you, choose at least one tool for each, and provision contacts, keys, hardware, and permissions in advance. Then test each condition separately: no internet, filtered internet, intermittent connectivity, servers unreachable, limited physical range. Turning the internet off tests only the first.

## Guides and Threat Models
- [EFF Surveillance Self-Defense](https://ssd.eff.org/) - Practical security guides for protesters, journalists, and other at-risk users. By the Electronic Frontier Foundation.
- [net4people/bbs](https://github.com/net4people/bbs) - Multilingual forum and reading list on censorship-circumvention research and deployment reports.
- [Security in a Box](https://securityinabox.org/) - Digital-security guides for human rights defenders. By Front Line Defenders.

## Organizations
- [Access Now Digital Security Helpline](https://www.accessnow.org/help/) - Free 24/7 security helpline for civil society, run by the organization behind the #KeepItOn shutdown-tracking coalition.
- [Association for Progressive Communications](https://www.apc.org/) - Long-running network supporting community networks and connectivity rights worldwide.
- [Internet Society Community Networks](https://www.isocfoundation.org/grant-programme/community-centered-connectivity/) - Grants and technical support for community-owned connectivity. Co-developed the LibreRouter.
- [NetHope](https://nethope.org/) - Coalition of NGOs and technology companies that restores connectivity after disasters. Ran 90 Wi-Fi sites across Puerto Rico after Hurricane María.
- [Télécoms Sans Frontières](https://www.tsfi.org/) - Emergency telecom NGO that has deployed satellite connectivity alongside first responders since 1998.

## Developer Resources
- [p2panda](https://p2panda.org/) - Rust toolkit for building local-first, disruption-tolerant applications. **Experimental**
- [The ONE Simulator](https://github.com/akeranen/the-one) - The standard academic simulator for testing delay-tolerant and opportunistic routing protocols before deploying them.
- [Willow Protocol](https://willowprotocol.org/) - Sync protocol and data model for offline-first applications with fine-grained capabilities. In the Earthstar lineage. **Experimental**

## Graveyard
*Projects that shaped resilient communication and are no longer maintained. Kept for the record. Domains of dead projects sometimes get squatted or hijacked. Where that happened, links point to archived copies.*

- [Byzantium Linux](https://github.com/Byzantium/Byzantium) - Bootable live distribution that turned any laptop into a mesh node with no configuration. **Discontinued!**
- [Commotion Wireless](https://github.com/opentechinstitute/commotion-router) - State Department-funded mesh firmware from the Arab Spring era. Its Red Hook offshoot in Brooklyn survived Hurricane Sandy. **Discontinued!**
- [disaster.radio](https://github.com/sudomesh/disaster-radio) - Solar-powered LoRa mesh for post-disaster networking. Its maintainers point to Meshtastic and Reticulum as successors. **Discontinued!**
- [OpenCellular](https://github.com/Telecominfraproject/OpenCellular) - Facebook's open cellular base-station platform. Stewardship passed to the Telecom Infra Project and stalled. **Discontinued!**
- [PirateBox](https://github.com/PirateBox-Dev/PirateBoxScripts_Webserver) - Offline Wi-Fi box for anonymous local file sharing. It started a whole genre. ShareBoxx is a maintained successor. **Discontinued!**
- [Serval Project](https://github.com/servalproject/serval-dna) - Early disaster mesh telephony for Android. Its Rhizome store-and-forward design is still influential. Unmaintained since about 2022. **Discontinued!**
- [TapDance](https://github.com/refraction-networking/tapdance) - First ISP-deployed refraction-networking design. Superseded by Conjure. **Discontinued!**
- [Taylor UUCP](https://www.gnu.org/software/uucp/) - The classic Unix store-and-forward transport that carried mail and Usenet over intermittent links. NNCP is its modern successor. **Discontinued!**
- [Village Telco](https://villagetelco.org/) - The Mesh Potato combined a mesh Wi-Fi node with an analog phone port for community telephony. Hardware discontinued. **Discontinued!**

## Other Related Lists
Deeper dives into single technologies that this list covers only for their resilience role:

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
- [awesome-offline-knowledge](https://github.com/gdamdam/awesome-offline-knowledge) - This list's sibling: keeping knowledge accessible without the internet.
- [awesome-privacy](https://github.com/Lissy93/awesome-privacy) - Privacy-respecting software, including encrypted messengers.
- [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) - Self-hosted server software, including communication systems.

## Contributors

Thanks to [all contributors](https://github.com/gdamdam/awesome-resilient-communication/graphs/contributors). Contributions are welcome. See the contributing guide above.

This work is dedicated to the public domain under [CC0 1.0](LICENSE).
