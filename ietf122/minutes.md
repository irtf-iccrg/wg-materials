# IETF 122 - ICCRG

Monday 17^th^ March 2025, 09:30 - 11:30 ICT
Location: Boromphimarn 4
Note taker Simone Ferlin-Reiter (Red Hat), with help from Mohit Prakash Tahiliani (National Institute of Technology Karnataka, Surathkal) and Stuart Cheshire (Apple)

## Agenda items

- LEDBAT++ - draft-irtf-iccrg-ledbat-plus-plus-02 - Chairs, 5 minutes
- Pacing in transport protocols - draft-welzl-iccrg-pacing Michael Welzl, remote, 10 minutes
- Mind the Misleading Effects of LEO Mobility on End-to-End Congestion Control - Zeqi Lai, 20 minutes
- Improving Cloud Gaming traffic QoS: a comparison between class-based queuing policy and L4S - Thibault Cholez, 20 minutes
- Adapting Home Routers to Congestion Control’s Reactions for Consistent Low Latency - draft-zhang-iccrg-confucius - Zili Meng, 15 minutes
- Challenges in Networking for AIML clusters - Costin Raiciu, 45 minutes

## LEDBAT++, Reese E. (on behalf of authors)

Document ready for Research Group Last Call, so that everyone has another chance to read the document and share their thoughts after the meeting.

Reese: Does anybody have any comments, etc. to LEDBAT++?

## Pacing in transport protocols, Michael Welzl (MW)

Document on version 02 with a few updates:

Extend discussion on feedback from private emails (Ingemar J.) - SYN/ACK and RTTS, micro/tiny-bursts and a few other topics incorporated in the new version.

M.W.: When is the document ready for adoption since the authors have seen interest in the past?

Gurtej Singh Chandok (Apple): Some real-time protocols rely on sending bursty traffic to determine the bottleneck capacity. Smoothing out bursts interferes with that.

Lars Eggert (Mozilla): Thinks that the document is ready for adoption.

Christian Huitema (Private Octopus, Inc.): He's seen deviations from pacing in applications are (traffic) limited.

MW: This will be incorporated in the document.

Lucas Pardue (Cloudfare) via chat: I can't think of a reason you wouldn't adopt this.

## Mind the Misleading Effects of LEO Mobility on End-to-End Congestion Control, Zeqi Lai (ZL)

Geoff Huston (APNIC): BW and delay estimations seems to be diverging from others working on the same system. You report higher RTT and lower bandwidth values. 

ZL: Contention might also be an issue, as pointed out by G.H.

Zili Meng (HKUST): Another might be still using BBRv1 and remove the limit of the cwnd of 2xBDP?

Gurtej Singh Chandok (Apple): ML congestion controllers as pointed by you do not work well, is it because of training on the wrong data? Which lab environment did you use, can you share it?

ZL: We are not sure if changing to LEO networks would work. We do not use tools such as ns2, contact us offline

Gorry Fairhurst (University of Aberdeen): Have you done measurements with more than one flow, looking at congestion loss?

ZL: Not considered.

Stuart Cheshire (Apple): Three points:

1. Let’s all of us working in this area try to avoid using “performance” as a synonym for “throughput”. Network performance includes many considerations beyond throughput, including delay, packet loss, and other things. When we are talking specifically about “throughput” alone, let’s use that word.
2. Slide 15 mentions “Massive non-congestion network variations”. I’m not sure what that means. In this research group, the word “congestion” means, “sending data faster than the network can carry it.” If a satellite handoff makes the available capacity drop by a half, and the source keeps sending at the same rate, then the source is sending data faster than the network can carry it, and that is congestion.
3. You stated, without any evidence, that “links are lossy.” I think, if you carefully investigate the actual cause of loss, you will find that most links are very reliable and most losses are actually congestion losses (i.e., the source is sending data faster than the network can carry it.) For example, it is frequently claimed that holding your phone next to a microwave oven causes Wi-Fi packet loss. With a minimal superficial investigation — e.g., Wireshark shows packets going in to the Wi-Fi Access Point that do not arrive at the receiver — you may conclude that the microwave oven has made the Wi-Fi link become lossy. What is actually happening is that the microwave oven interference causes the Wi-Fi Access Point to adapt to the new conditions by lowering its transmission rate to maintain reliable transmission. While the sender contines to send packets at 600Mb/s into a Wi-Fi link that is now carrying 60Mb/s, it is not surprising that 90% of those packets will be lost. The microwave oven interference has not made the Wi-Fi link *unreliable*; it has made the Wi-Fi link *slower*. As long as the sender decides this is “non congestion loss” and consequently does not reduce its rate, then it will continue to lose 90% of its packets.

ZL: This packet loss is not caused by congestion / queueing.

Eric Kinnear (Apple): Switching between technologies is where I recommend to look at, due to drastic different capabilities offered by the networks.

## Improving Cloud Gaming traffic QoS: a comparison between class-based queuing policy and L4S, Thibault Cholez (TC)

Ingemar Johansson (Ericsson): Due to scream pacing you get lower bandwidth, it is expected.

Christian Huitema (Private Octopus, Inc.): Have you thought of testing with something other than L4S?

TC: The focus was really on L4S, no FQ-CoDel.

Greg White (CableLabs): Agreessive lazy target is perhaps the other reason for a lower throughput with scream. Try with a higher AQM target, i.e., you will see higher utilization. 

TC: A Nvidia platform (ininteligible?) has L4s available.

## Adapting Home Routers to Congestion Control’s Reactions for Consistent Low Latency, Zili Meng

Bjørn Ivar Teigen Monclair (Domos): It would be good to see work on using different congestion controls, and how the change the situation.

Stuart Cheshire (Apple): The graph shown on slide 8 seems overly simplistic. It shows that that when a web page load starts, the web page loading instantaneously starts using a specific constant amount of capacity, and the capacity available to the videoconference correspondingly drops instantaneously to a new lower level. This is not how the gradual ramp-up of TCP (or QUIC) slow-start works. The graph also shows that the videoconference rate-adaptation algorithm adjusts linearly to the reduction in available capacity. The principle of AIMD (Additive Increase, Multiplicative Decrease) has been used since the 1980s precisely to avoid congestion collapse, and causes senders to react rapidly to reductions in available capacity.

Ian Swett (Google): 20 flows is extremely common from browsers loading resources nowadays. More research on this space is welcome!

Michael Welzl (UOslo): How fast were these senders, i.e.,  how far were they from the bottleneck link?

ZM: Slide 7 this was amazon.com

Michael Welzl (UOslo): Did you look at the RTT of the flows in general (amazom.com)?

ZM: It does not make a big difference, small pages.

Michael Welzl (UOslo): OK, agree. Just curious.

## Challenges in Networking for AIML clusters, Costin Raiciu (CR)

Lars Eggert (Mozilla): We would like to have Costin taking more about it.

