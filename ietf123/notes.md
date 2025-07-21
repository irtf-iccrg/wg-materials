# ICCRG Research Group Agenda - IETF 123
Time and Date
Monday July 21, 17:00 - 19:00 CEST (See this time in your local timezone)
Location: Hidalgo

## Administrivia, Blue sheets / scribe selection / NOTE WELL

## Presentations

### Chair slides & Hackathon update - Chairs, 5 minutes
- Reese points to Mohit and refers to presentation in CCWG

### Looking at the interplay between congestion control algorithms and speed-test tools - Jason Livingood

- Mo Zanaty: What differences in latency did you see with universal AQM vs others? 

- Jason: Working latencies cut in half when we turned DOCSIS-PIE on in the core, that was a huge win. Dual queue on top was half again, see Stuart Cheshire's presentation, idle latency improved as well.

- Mo: Roughly same order in each phase?

- Jason: 50% reductions in each step, dual queue got you pretty close to idle latency.

- Alessandro Ghedini: <clarification question/>

- Jason: clarifies that change in behavior on slide 6 is when downstream AQM was activated

- Alessandro: Did things get better because the capacity changed?

- Jason: No, the capacity is the same, it's just the introduction of the dual queue AQM. A realtime flow prior to this change would lose to queue building traffic, now it's much better for interactive traffic.

- Alessandro: Any specific CCA you were testing with?

- Jason: Running DOCSIS PIE, not BBR
    (later in chat): the test originates on a CPE that has DOCSIS-PIE on its US interface and downstream hits the CMTS interface with same AQM. It is not limited by the CCA on the linux speed test server.

- Mohit Tahiliani: Slide 4, what do the different lines mean?

- Jason: Upstream and dowstream; dashed line is the "goal" what the tests were aiming for

- Neal Cardwell: number of parallel connections in the tests?

- Jason: thinks it could be 4, but is still subject to tweaking

- Neal: changing the number of connections might no longer reflect actual user performance

- Jason: external speed tests, such as Cloudflare, did not show any change. they might be using multiple connections, too

- Neal: These are different classes of test, first classic ECN, second mixed like you get with Apple + Linux, third is L4S

- David Black: Good to see the algorithms doing what they're supposed to do in practice, and at scale. Would strongly support measuring additional things, so that we can optimize it. Focus on what matters to the users.

- Jason: Agreed.


### Pacing in Transport Protocols (draft-welzl-iccrg-pacing) updates - Michael Welzl

- Show of Hands: I have read draft-welzl-iccrg-pacing (any revision)
    - Yes: 18
    - No: 13
    - Out of total: 59

- Show of Hands: I think ICCRG should adopt draft-welzl-iccrg-pacing?
    - Yes: 28
    - No: 0
    - No opinion: 6
    - Out of total: 61

- Reese: we will run formal adoption call on the list

### ACE: Sending Burstiness Control for High Quality Real-Time Communication - Zili Meng

- Neal Cardwell: choosing token bucket size such that it avoids packet loss? 

- Zili: yes

- Neal: It seems like we care about queueing delay in the middle of the network too, not just loss. How about combining with TSO and use a pacing rate that works well.

- Zili: Good point. Queueing delay in the middle network is equivalent to the queueing delay in the pacing buffer.

- Neal: Not equivalent. The influence to other competing flows will be different if burst out.

- Zili: worthwhile to consider in the future.

- Tongyu Dai: How is the quality not affected if the key frames are reduced?

- Zili: ACE does not reduce the key frames' sizes -- it adjusts the frame size of p-frames at the cost of additional encoding time instead of quality.

- Tongyu: Will the codes be open-sourced?

- Zili: will open source code before the SIGCOMM conference

- Jana: have you done experiments with multiple senders using your scheme?

- Zili: only initial experiments, there will be interactions between these senders. we have thus far mainly checked with other senders

- Mo Zanaty: do you integrate your bucket with the buckets of the encoders?

- Zili: our buffer is after the encoders

### Tutorial/Panel (45 minutes):
#### Real-time, live video delivery - Ali C. Begen

- Jana: What are the sender-side signals you are using?

- Ali: It could be any defined signal

- Jana: Is this theoretical or are you doing it?

- Ali: Implemented.

- Mo Zanaty: there is no established way for senders to have receiver-side view and vice versa. We currently have application-specific solutions to this problem. might be interesting to aim for a generic signaling solution

- Ali: this is a transport layer-independent challenge as it also depends on info provided by application layer 

- Jana: follow-up to Mo. Streaming is a particular kind of application that can enable this

#### Sammy: smoothing video traffic to be a friendly internet neighbor - TY Huang

- Tongyu Dai: Is ABR implemented on client-side? How combined with CC on server-side?

- TY: Did this on client-side.

- Tongyu Dai: Traffic will coexist with other services or applications. How do you ensure everyone will be "nice"?

- TY: Services or applications have to keep each other in check.

- Alessandro Ghedini: How exactly does the interaction work? Do you always pace at the maximum? What is the time frame?

- TY: We do this on segment level. Tell congestion control what maximum speed we need.

- Jinghao Yuan: What's the interaction between client and server?

- TY: We have a side channel.

- Will Law: Netflix/Youtube have lucky position that they control sender and receiver. There are also standards for CDNs (who don't control clients) and clients (who don't control servers) to exchange/retrieve information. Akamai would like to provide this capability if there's interest. Would be great to look at interop possibilities.

- Mo Zanaty: There needs to be a more fine-grained API between CCA and application to resolve issues that are for example highlighted by seemingly conflicting proposals (refers to ACE presentation)

- TY: We aim for combined logic, not two different ones that communicate via API

- Jana: Not sure there's anything to standardize here. But the talk shows that CC and applications can work together

- Jason: CC landscape was ossified for long time. Streamers had to find new ways to address this. Good to see progress and that new flexibility on transport can help. Interesting where the equilibrium will be.

- Simone: Part of the intention of this panel was to illustrate the problem. We have the opportunity to create documents in this group. Could be benchmarking or otherwise. Let's continue the discussion.
