# Déploiement d'une infrastructure VoIP en environnement virtualisé

. Déploiement complet d'une infrastructure de téléphonie sur IP professionnelle, avec analyse de sécurité et de qualité de service.

## Contexte

Comment déployer, sécuriser et superviser une infrastructure VoIP professionnelle dans un environnement virtualisé, en garantissant la confidentialité des communications, la qualité de service et la détection des menaces réseau ?

Ce projet répond à cette problématique à travers six objectifs opérationnels : mise en place de l'architecture réseau, déploiement d'un serveur de téléphonie, implémentation d'une politique de Qualité de Service (QoS), chiffrement de bout en bout, capture et analyse du trafic réseau, et détection d'intrusion.

## Architecture

- Segmentation en 3 VLANs : Management VoIP (CUCM + station d'analyse), Softphone 1, Softphone 2
- Routage inter-VLAN via Router-on-a-Stick
- Serveur de téléphonie **Cisco Unified Communications Manager (CUCM) 14**
- Softphones **Cisco IP Communicator (CIPC)** sur postes Windows 10
- Station d'analyse dédiée (Wireshark) connectée en port SPAN

## Technologies utilisées

- **CUCM 14** — plateforme de téléphonie centrale (Proxy SIP, Registrar)
- **Protocole SIP** — signalisation des sessions d'appel
- **RTP/RTCP** — transport du flux audio en temps réel
- **QoS DiffServ (DSCP, LLQ)** — priorisation du trafic voix
- **TLS / SRTP** — chiffrement de la signalisation et du flux audio
- **Wireshark** — capture et analyse du trafic
- **GNS3 + VMware Workstation** — environnement de virtualisation

## Ce qui a été réalisé

- Segmentation réseau en VLANs avec routage inter-VLAN et NAT
- Configuration complète du CUCM (services, Device Pools, Dial Plan, SIP Profiles)
- Déploiement et enregistrement de deux softphones CIPC (extensions 1001/1002)
- Politique de Qualité de Service avec marquage DSCP EF (voix) et CS3 (signalisation), file d'attente LLQ
- Capture et analyse Wireshark de la signalisation SIP et des flux RTP
- Validation du chiffrement TLS (port 5061) et SRTP pour sécuriser la voix et la signalisation

## Résultats / Tests

- Enregistrement SIP réussi des deux softphones (statut *Registered* confirmé dans la console CUCM)
- Appels bidirectionnels validés avec transmission audio G.711
- Séquences SIP complètes observées via Wireshark (REGISTER → INVITE → 180 Ringing → 200 OK → ACK → BYE)
- Fonctionnement du LLQ confirmé : paquets RTP correctement priorisés avec marquage DSCP EF (46)

## Limites et pistes d'amélioration

Ce projet de lab présente des limites par rapport à un environnement de production : la confidentialité des communications et la détection des menaces nécessitent un chiffrement systématique (TLS/SRTP) et un IDS dédié (Suricata) pour couvrir l'ensemble des risques d'une infrastructure VoIP d'entreprise moderne.

## Rapport complet

📄 [Rapport technique complet (PDF)](Rapport-VOIP-CUCM.pdf) — cadre théorique, architecture détaillée, configuration pas à pas, analyse des résultats.
## Auteurs

Projet réalisé en groupe :
- **Priva EKORE MINANG**
- Michel Rickiel OBIANG ASSOUME
- Yann Christopher OBAME MBA

[LinkedIn](https://www.linkedin.com/in/) · [GitHub](https://github.com/privaekoreminang)
