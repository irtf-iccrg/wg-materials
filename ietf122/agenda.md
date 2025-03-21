# ICCRG Research Group Agenda - IETF 122

## Time and Date

* Monday March 17, 09:30 - 11:30 ICT ([See this time in your local timezone](https://www.timeanddate.com/worldclock/fixedtime.html?msg=ICCRG+at+IETF+122&iso=20250317T0930&p1=28&ah=2))
* Location: Boromphimarn 4
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

- **Chair slides & Hackathon update** - _Chairs_, 5 minutes
- **LEDBAT++** - [draft-irtf-iccrg-ledbat-plus-plus-02](https://datatracker.ietf.org/doc/draft-irtf-iccrg-ledbat-plus-plus/) - _Chairs_, 5 minutes
- **Pacing in transport protocols** - [draft-welzl-iccrg-pacing](https://datatracker.ietf.org/doc/draft-welzl-iccrg-pacing/) - _Michael Welzl_, remote, 10 minutes
- [**Mind the Misleading Effects of LEO Mobility on End-to-End Congestion Control**](https://dl.acm.org/doi/abs/10.1145/3696348.3696867) - _Zeqi Lai_, 20 minutes
- [**Improving Cloud Gaming traffic QoS: a comparison between class-based queuing policy and L4S**](https://inria.hal.science/hal-04594817/document) - _Thibault Cholez_, 20 minutes
- **Adapting Home Routers to Congestion Control’s Reactions for Consistent Low Latency** - [draft-zhang-iccrg-confucius](https://datatracker.ietf.org/doc/draft-zhang-iccrg-confucius/) - _Zili Meng_, 15 minutes
- **Challenges in Networking for AIML clusters** - _Costin Raiciu_, 45 minutes

## Challenges in Networking for AIML clusters

### Abstract
Despite the commonly held belief that the network is not the bottleneck in datacenters, training machine-learning workloads is network bound and has lead to the deployment of fully provisioned folded Clos topologies. Even so, in production that communication makes up 15% to 75% of training time depending on the model, and this is expected to become worse as training clusters increase in size; worse, existing transports fail to properly utilize the available core capacity.
We analyze in detail how we can improve networking for AI/ML training, with a particular focus on understanding how to build an efficient multipath transport protocol and congestion control to achieve good performance for difficult collective communications such as all-to-all. We will give an overview of the Ultra Ethernet Consortium, a novel standardisation body that is defining the transport for AIML networks.

### Bio

Costin Raiciu is Chief Architect in Broadcom's Core Switching Group and Professor at University Politehnica of Bucharest where he leads the Netsys group. Costin has received his B.Sc. and M.Sc. from University Politehnica of Bucharest in 2003 and 2004, and his PhD from University College London in 2011. Costin's work is at the area of networking, operating systems and verification. His main work includes design and implementation of Multipath TCP [RFC8684, RFC6356], lightweight virtualization (LightVM [SOSP17] and FlexOS [ASPLOS22]) and verification (Symnet[SIGCOMM'16], BF4 [Sigcomm'20]).   Costin is very keen on pushing his research work into production, with Multipath TCP a prime example of deployed work. Costin is now part of the team standardizing next generation networking at the Ultra Ethernet Consortium, a protocol that is partly based on his prior work called EQDS (NSDI'22).
