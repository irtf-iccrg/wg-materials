# ICCRG Research Group Agenda - IETF 126

Time and Date
– Wednesday July 22, 09:00-11:00 CEST
Location: Park Suite 7

# Presentations
Chair slides & Hackathon update - Chairs, 5 minutes
Note taker: Ike Kunze

## Pacing in Transport Protocols, draft-irtf-iccrg-pacing - Michael Welzl, on-site, 5 minutes
Michael Tüxen: there’s a special number from Apple (burst size of 244 microseconds worth of data). would be cool to know where it comes from.

Christian Huitema: trade-off between Prague-related considerations (avoiding bursts) and the need of some minimum burst size (of 10 packets) for GSO to be effective. could be that Apple has based it on this.
Michael Tüxen (proxy for someone else): number is 1/4096.

Chat:

– Alan Jowett: 244us is approximately the reciprocal of 4096 so, 4096 times per second == 244us

– Michael Welzl: Yes - probably: 1) less than 1ms, to avoid the bursts for L4S as Christian said, 2) why not 1/4, for example; 3) let’s implement 1/4 efficiently in the kernel.

## Windowless Cumulative ACK Extension for RDMA Retransmission, draft-chen-rdma-windowless-ack - Danyang Chen, remote, 5 minutes
No questions

## Testing Congestion Control and Queue Management Mechanisms, Mohit Tahiliani, on-site, 15 minutes
Simone: what about an evaluation framework for congestion control?

– Mohit: still working on an evaluation suite that is compliant to RFC 9743

## Using Little’s law queueing theoretic approach as congestion window update, Dumisa Ngwenya, on-site, 20 minutes
Roland Bless: high throughput, low delay not mutually exclusive. did you test together with loss-based congestion control as delay-based usually gets supressed? Did you test on wifi?

– Dumisa: Have not yet tested with loss-based, will likely increase base RTT, might cause instability. ensured that we can quickly measure the RTT.

– Roland: make sure to test with (artifical) jitter because that could be challenging for the algorithm.

## MOONCAKE: trading more storage for less computation — a KVCache-centric architecture for serving LLM chatbot, paper, Mingxing Zhang, remote, 30 minutes
Simone: Red Hat uses MOONCAKE as a test case for how LLM systems behave as an application

## Managing Congestion Control Heterogeneity on the Internet with Approximate Performance Isolation, paper, Ayush Mishra, on-site, 20 minutes
Jana Iyengar: FQ needs per-flow state. Does Santa also have per-flow state?

– Ayush: yes, needs per-flow state.

– Jana: comparison to L4S?

– Ayush:

Roland Bless: having a mice queue is a problem, could get problem with reordering. How do you classify mice flows?

– Ayush: first 20 packets go into mice queue.

– Roland: have you looked at slowdown due to reordering?

– Ayush: have not looked at slowdown, but looked at reordering. Reordering basically not happening. Order of shuffling has an impact.

Stuart Cheshire: +1 to point that too many people prioritize having more throughput. Latency/throughput not mutually exclusive, good that the paper also says that. L4S, Prague, etc. should be considered in more research papers. Comment about “flows lying about their L4s compliance”: L4S not about “better treatment”, it’s about getting better informatuion about queue/network state

Chris Box: comparison to FQ. What is the impact in terms of resource use. Probably less memory, what about CPU?

– Ayush: Have built this in P4 switch, so CPU cycles not really applicable. Regarding memory, not sure that it actually needs less memory.

Danesh Zeynali: have you tried this with multiple bottlenecks? touching the flow on first bottleneck could affect behavior on the next?

– Ayush: no, not yet, but interesting dimension.

– Danesh: what about flows with different RTTs, how do you setting the fair queuing for these?

– Ayush: Santa does not care about the RTT / focus on RTT fairness specifically

Gorry Fairhurst: look at more queues, not just 1/2, maybe a handful. complexity to implement this compared to L4S?

– Ayush: not too complicated to implement but did not check in terms of L4S

– Gorry: have you considered impact on “harm”?

– Ayush: not really focused on harm, yet

Mohit Tahiliani: have you tested with 90 flows max?

– Ayush: only tested with 90 flows

– Mohit: this compares with FairQueuing. There is also FlowQueuing. FlowQueuing has specific properties, e.g., for sparse flows. Maybe worth taking that into account

– Ayush: came across lots of concepts. here, we have a single Mice queue

– Mohit: flowqueuing has multiple queues for mice flows with different priorities

Michael Welzl: flowqueueing; sparse flows might essentially live “without a queue”. In Santa, these sparse flows might be pushed together with other flows into one queue.

– Ayush: have special handling for short/sparse flows but such parameters could affect the described behavior.

Jana Iyengar: when mentioned FQ, meant flowqueuing. have you looked at how applications (with multiple flows) can game the system?

– Ayush: not yet.