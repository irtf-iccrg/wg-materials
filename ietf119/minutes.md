# ICCRG - IETF 119

## Revisiting Common TCP Evaluation Suite - David Hayes

Colin Perkins (as individual): This is nice, good thing to have. I agree with the comment about focus. ECN etc is nice and all, but it also needs to be finishable in the next decade. How much is TCP-specific in this draft?

David: This is not really TCP-specific, just looking for a reactive congestion control. TMIX was designed to work with TCP, but it can be anything that can read an application interaction file and process it, so it doesn't have to be TCP.

Colin: Suggest to change the phrasing to be more generic. If it is possible to update this to support QUIC, it would gather a lot more interest.

Zili Meng: Have you given consideration to video-like and inelastic traffic?

David: Me personally, No. But on the Internet, there's a portion of elastic and inelastic traffic. What we do is not going to be exactly what's happening on the Internet. It's more that the traffic reproduces the characteristics that matter to test, we'd like to have the same proportion of traffic, how is undecided. 

Zili: Maybe we can add this, it's similar to on-off application in ns-3 but video conferencing is elastic, it is not inelastic. 

David: This is good, I'm sure Tom and Mohit would love to have you contribute. The tests are based on real traffic traces, so we have to take the real traffic, measure it, then convert it to the application.

Zili: Many applications have different patterns, such as web etc, is this a consideration?

David: The consideration would be, does this traffic pattern change the dynamic in an important way, does it introduce a characteristic that is important to test?

Shiva Raj: There have been lots of new CCs. In ns-3, if I want to simulate BBRv3 over WiFi, will this follow?

David: This does have a Wifi test. The idea is to have something really light for someone who wants to test their CC, they can just plug it in here, it should just run and give them their result, just take the actual CC. So in your example, you'd be running BBRv3 for every TCP session.

Christian Huitema: Have you been looking at the work that is ongoing to rewrite 5033bis defining the criteria for CC to check? There's a set of criteria and specific tests in there. Could someone use this tool to assess the criteria in 5033bis?

David: This draft and 5033 have a common background in Sally Floyd's work, many of those tests are there...

Christian: In 5033bis there is a departure from Sally Floyd's work. There was a lot of emphasis on equality of bandwidth, and in 5033bis the focus has shifted to not causing specific harm, e.g. losses, bufferbloat

David: Because this is 10 years old at this point, some of those tests are there already. We hope the community will refine it and bring in some of those ideas, maybe more strongly the latency type ones. But this is not meant to test whether it's Internet-ready, this is meant to provide a comparison between new experimental congestion controls that are probably a long way from CCWG.

Reese Enghardt: Sound like there is interest in testing CC. This reminds me of why we have CCWG now: Congestion control has changed and the Internet has changed over the last years, I see this as a cause why we're getting these additional things brought up now. Who is interested in doing work in this space in ICCRG? Work in this space can mean work on this particular implementation but also it can mean show up at a hackathon in Vancouver and talking about different testbeds, testing tools, simulations.

Who is interested in doing work in this space in ICCRG? Show of hands: 13 Yes

David: I would like to see a group convene on the list to talk about how to progress this.

## Implicit Congestion Notification: Achieving Consistent Low Latency for Wireless Real-Time Communications with the Shortest Control Loop - Zili Meng

Vidhi Goel: Interesting idea. If you delay packet number 4, if packet 4 was the end of a resource, so the resource could have loaded earlier if it hadn't been delayed. Not saying that that's always gonna happen, just talking about how HTTP resources are divided into different streams over QUIC or by sequence numbers. Second, How do you solve this problem for loss-based CC? Third point, delayed ack can also cause probes to be sent, like TLP, if you wait long enough it can cause RTO.

Zili: We don't delay the ack by long, just by 5 ms is good enough, not by 100ms or so, which would trigger RTO. Loss based is out of scope for this paper, as we design for delay-sensitive applications like videoconferencing and cloud gaming, we understand those don't use loss-based CC.

Alper Demir: What has implicit congestion notification to do with shifting the delay curve forward?

Zili: Here we apply what we measure on the downstream. ICN is simply what we called that mechanism to apply the delay gradient on the reverse direction.

Shiva: You inject a delay, what is its impact on performance?

Zili: We are deliberately slowing the rate so as to match the link rate.

Shiva: Did you try with L4S?

Zili: Yes, L4S itself doesn't solve this problem, but it responds well.

Christian: Suppose you could ECN mark that you have seen reverse path congestion, would that work?

Zili: Yes, though of course many CCs don't support that.

Christian: Nasty wifi congestion mechanism, card goes to sleep for 100ms or so, and there are no packets in either direction. Have you tested this?

Zili: We saw this too. We don't have an answer at this time.

Randell Jesup: You should probably look at testing against LEDBAT. How are you handling WebRTC and related protocols, since they're not ACK based.

Zili: We didn't cover that in this presentation, but we modify the payload.

Randell: Have you thought about whether it is good to combine this with ECN, or would you get a double-impact?

Zili: For some CCs, that can improve results still further.

Jonathan Kua: Have you tested with multiqueue AQM like FQ-CODEL?

Zili: Great question... not in this paper, but there is a followup to it in which we do.

## rLEDBAT

Vidhi presents.

Reese: Who has read the rLEDBAT draft? Show of hands: 6 Yes

Colin Perkins: It seemed to be in good shape some time ago. Probably just needs a review and should proceed.

Reese: Looking to last call this after the meeting.
