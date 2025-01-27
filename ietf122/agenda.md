# ICCRG Research Group Agenda - IETF 122

## Time and Date

* TBD
* Location: TBD
* [IETF Agenda Link](https://datatracker.ietf.org/meeting/122/agenda/?show=iccrg)

## Links

* [Onsite Tool](https://meetings.conf.meetecho.com/onsite122/?session=33504)
* [Meetecho Room](https://meetings.conf.meetecho.com/ietf122/?group=iccrg&short=iccrg&item=1)
* [Meeting chat](https://zulip.ietf.org/#narrow/stream/iccrg)
* [Notes](https://notes.ietf.org/notes-ietf-122-iccrg) 
* [Minutes](https://datatracker.ietf.org/doc/minutes-122-iccrg/)

## Administrivia

* Blue sheets / scribe selection / [NOTE WELL](https://www.irtf.org/policies/irtf-note-well-2021-05.pdf) 
* Agenda revision

## Presentations

- Chair slides - _Chairs_, onsite, 5 minutes
- **Hackathon update** - _Chairs_, 5 minutes
- **Mind the Misleading Effects of LEO Mobility on End-to-End Congestion Control** - _Zeqi Lai_, 20 minutes
- **Improving Cloud Gaming traffic QoS: a comparison between class-based queuing policy and L4S** - _Thibault Cholez_, 20 minutes
- **Challenges in Networking for AIML clusters** - _Costin Raiciu_, 45 minutes

## Challenges in Networking for AIML clusters

### Abstract
Despite the commonly held belief that the network is not the bottleneck in datacenters, training machine-learning workloads is network bound and has lead to the deployment of fully provisioned folded Clos topologies. Even so, in production that communication makes up 15% to 75% of training time depending on the model, and this is expected to become worse as training clusters increase in size; worse, existing transports fail to properly utilize the available core capacity.
We analyze in detail how we can improve networking for AI/ML training, with a particular focus on understanding how to build an efficient multipath transport protocol and congestion control to achieve good performance for difficult collective communications such as all-to-all. We will give an overview of the Ultra Ethernet Consortium, a novel standardisation body that is defining the transport for AIML networks.

### Bio

Costin Raiciu is Chief Architect in Broadcom's Core Switching Group and Professor at University Politehnica of Bucharest where he leads the Netsys group. Costin has received his B.Sc. and M.Sc. from University Politehnica of Bucharest in 2003 and 2004, and his PhD from University College London in 2011. Costin's work is at the area of networking, operating systems and verification. His main work includes design and implementation of Multipath TCP [RFC8684, RFC6356], lightweight virtualization (LightVM [SOSP17] and FlexOS [ASPLOS22]) and verification (Symnet[SIGCOMM'16], BF4 [Sigcomm'20]).   Costin is very keen on pushing his research work into production, with Multipath TCP a prime example of deployed work. Costin is now part of the team standardizing next generation networking at the Ultra Ethernet Consortium, a protocol that is partly based on his prior work called EQDS (NSDI'22).
