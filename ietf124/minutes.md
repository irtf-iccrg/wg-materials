# ICCRG Research Group Agenda - IETF 124

Tuesday November 4, 14:30 - 16:30 EST
Location: Van Horne

## Administrivia
Note takers: Stuart Cheshire, Greg White

## Chair slides & Hackathon update - Chairs, 5 minutes


## Pacing in Transport Protocols

_Michael Welzl_, [slides](https://datatracker.ietf.org/meeting/124/materials/slides-124-iccrg-pacing-in-transport-protocols-draft-irtf-iccrg-pacing-00-00), [draft-irtf-iccrg-pacing](https://datatracker.ietf.org/doc/draft-irtf-iccrg-pacing/)

Michael Welzl gave presentation on pacing in transport protocols. Addressed old research paper that purports to show that pacing TCP packets causes problems; in reality the paper observed a problem but investigation to understand the true root cause was lacking.

Gorry Fairhurst (University of Aberdeen): Promised to review the draft and send comments, including input relating to QUIC and the UDP-based interface.

## Congestion Notification for Multi-Resource Allocation Control

_Mario Patetta_, [slides](https://datatracker.ietf.org/meeting/124/materials/slides-124-iccrg-congestion-notification-for-multi-resource-allocation-control-00)

Mario Patetta presented information about resource allocation, using the example of 5G Network Slicing.

Stuart Cheshire (Apple): Slide 8 defines "congestion". To me, congestion is the desirable state of the network, it means the network is not idle. What does it mean to "lose" a resource?

Mario: This is another layer, multi-resource congestion. In our definition, if several resource controllers agree to allocate a resource to a certain service, and one of the controllers or segments is not able to provide the exact resource anymore. It might not be the correct word.

Stuart: So the loss over allocation means, you've overcommitted and then you can't deliver.

Ingemar Johansson (Ericsson): Using the term "congestion" is misleading. There is a disconnect between IETF and 3GPP about what that terms means. Is in-band signaling the most appropriate? Couldn't this be done out-of-band?

Roland Bless (Karlsruhe Institute of Technology: You say this works for any kind resource, but since the information is carried in the IP packets, the resource must be

Altanai Bisht (Cisco): What prevents fraudulent signalling of “congestion” that is not real, to manipulate resources? How can we make this safe?

Mario Patetta: This is for resource controllers that are supposed to cooperate.

Altanai Bisht (Cisco): So, this is for small environments where all devices are trusted because they belong to the same organization.

Gorry Fairhurst (University of Aberdeen): Does every packet carry these signals?

Mario Patetta: Every packet, in both directions.

Gorry Fairhurst: Using the DiffServ field for this prevents its use for other purposes (same with EXP bits)

Ruediger Geib: Does this assume that packets follow the same path in both directions?

Mario Patetta: Even if the path is non-symmetrical, the signal will eventually reach one of the endpoints.

## L4S and Prague update

_Koen De Schepper_, [slides](https://datatracker.ietf.org/meeting/124/materials/slides-124-iccrg-l4s-and-prague-update-00)

Stuart Cheshire: Clarification about not having to delay packets on slide 4: Rate management without queuing implies a connection that can support a higher data rate than the policer allows. You still need queuing if there's a physical bottleneck that cannot send higher than the data rate.

Koen: Yes, in the past you had to provide a shaper and a queue to limit that rate, you can now have a marking policer. Also sometimes a queue is needed because the network needs it (e.g. aggregation for efficiency)

Chris Box (BT): Clarification - On slide 4, you have an arrow marked SRM, static rate management, the flow in pink does the CE marking, and then that goes into a queue, and if everything goes correctly, the queue should be very short.

Koen: Think of it like a dualPI2 bottleneck, but the L4S path is a simple rate-based marker instead of a queue, it has priority in terms of latency.

Jonathan Lennox (8x8 / Jitsi): What does it fall back to if L4S is not available?

Koen: Currently Reno, but could use Cubic.

Martin Duke (Google): This is an important document. It seems like a template to be applied to congestion control algorithms, rather than specifying a congestion control algorithm itself. It seems to assume a loss-based congestion control algorithm. Not sure how it would work with a delay-based congestion control algorithm.

Koen: We need to rework the draft, it still talks about a research project. This work is now more concrete and we drive it to something which can be deployed.

Vidhi Goel (Apple): This could be applied to BBR.

Martin Duke (Google): I would like to know how to do that.

Koen: It can be used with delay-based congestion control algorithm by calculating both congestion windows independently, and then using the lower of the two calculations.

Martin: I look forward to the next version of the draft and implementing off of it.

Koen: It'll be good if people start using this and give feedback how they did it and how these APIs work. We implemented it in user space, so it should be easy for people to use.

Gorry: Slide 21 showing video encoding is confusing. We are using the congestion controller to find a rate for ABR?

Koen: It is a example of how a real-time video application can use the rate estimation from the PragueCC module to set the codec rate on a per-frame basis. These are just examples, there are different ways to use it.

Stuart: I agree with Gorry, we need to discuss these assumptions more.

Neal Cardwell (Google): There is more than just one "right" way to respond to Accurate ECN signals. BBRv2 would not interoperate well with Prague over the public Internet. There is future work to be done here. If would be good if the draft included guidance for other implementers saying how to make their congestion control algorithms compatible with Prague. There is an interesting [2005 SIGCOMM paper](https://dl.acm.org/doi/10.1145/1090191.1080098) on using utilization as the input to a rate manager algorithm.

Vidhi Goel (Apple): Should people be using the current BBRv2 and BBRv3 code for handling ECN?

Neal Cardwell (Google): No. That code is only suitable for data center use.

Vidhi: Do you plan to have something added to BBRv3?

Neal: Yes, but right now it's not staffed. If there are others out there interested in working on it, I'd be happy to collaborate.

Ingemar Johansson (Ericsson): You need to have buffering on the sender side. Video encoders like VP8 can be sluggish adapting their data rate.

Stuart Cheshire: Some video encoding applications could also compress frames on demand (at transmit time or shortly before), and thus send at a variable frame interval. You were describing a different programming model where the video encoder is a free-running process at a specific frame rate, and then it doesn't adapt very quickly. There are a lot of ways this can be done depending on system constraints, etc.

Roland Bless (Karlsruhe Institute of Technology): Did you test on 10Gb/s links? 100Gb/s?

Koen: I don’t have all that data here, but yes. Even at high rates it complete well with Cubic, or even out-competes Cubic. And only create 1ms.

Roland: On high speed links, there can be issues like jitter that is introduced by the kernel which makes it difficult to get congestion control to work well

Koen: Our variables all need to be big enough, we had an issue with the increment we calculated.

Stuart: Thank you again Koen for all this amazing work. We disagree on some details, but we have good discussions. I look forward to seeing this widely deployed on the Internet, it'll be a game changer.

Reese: I look forward to seeing the updated draft.
