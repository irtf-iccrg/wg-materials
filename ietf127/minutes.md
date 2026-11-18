# ICCRG Research Group Agenda - IETF 127

* Monday November 16, 09:00 - 11:00 PST
* Location: Golden Gate 4-5
* [Recording](https://www.youtube.com/watch?v=rEm8PiKBISk&list=PLAmA-Zfgwrso)
* Note taker: **Mohit P. Tahiliani**

# Presentations
Chair slides & Hackathon update - Chairs, 5 minutes

## Hackathon Update

Reese provided a quick update on the topics covered during the hackathon on Testing Congestion Control and Queue Management Algorithms. A more detailed update on the hackathon will be provided by Mohit in the CCWG meeting later in the week.

## Improving Evaluation of Heterogenous Congestion Control Algorithm Interactions

* Speaker: **Ranysha (Ray) Ware**
* [Paper](https://dl.acm.org/doi/10.1145/3789240.3829156)
* [Slides](https://datatracker.ietf.org/meeting/127/materials/slides-127-iccrg-improving-the-evaluation-of-heterogenous-congestion-control-algorithm-interactions-00)

* **Te-Yuan Huang**: Related to measuring harm around/after the convergence -- some applications download assets differently (using different CC algorithms). So in the aggregate, how do you measure harm at the application level? 
* **Ranysha**: One focus of our work is pretending that an application doesn't exist, and thinking about the CCA in isolation. It is definitely something to think about in terms of "at the application layer what are the differences". No answer for it as of now.

* **Esteban Carisimo**: This work is focusing on competing flows; which is sometimes missing in some of the lab tests. One of the challenges when we try to reconcile lab tests with production traffic, is the arrival rate, what is the status of this connection, etc. How do you think we can still make progress from the point that our simulations don't match what we see in real traffic.
* **Ranysha**: Perhaps, a better approach in the future would be to look at it at the application level. 

* **Sebastian Rust**: When we simulate delay based CCAs, we often see oscillations when they are competing. Could I use your metric to characterize the harm?
* **Ranysha**: The basic idea of relative harm is to come up with some way to measure the impact that one has on another. You can kind-of quantify oscillations in that way. It should fit within the framework.

* **Lars Eggert**: This seems to for throughput and long lasting flows. The web has changed since quite some time. It looks like the framework would apply to metrics like the time to first byte, is there another paper that you are working on that covers these metrics?
* **Ranysha**: We noticed that weird things happen when you put some of the metrics in the harm framework, kind-of a constraint that we have with a number that ends up between 0 and 1. So the idea was to continue improving what was already there (throughput for long lasting flows).

* **Christian Huitema**: +1 on what Lars said. The long term application that we are most concerned with is video; hence the evaluation of latency is as important, if not more, than the evaluation of bandwidth. 
* **Ranysha**: Yes, I need to think more about how to incorporate latency and other metrics in the framework.

* **Antonio Vicente**: Do you consider other things like the convergence time? any harm that we can get from a long convergence time? 
* **Ranysha**: Yes, if you could come up with the calculations to put in the framework, it would work as well.

* **Apoorv Kothari**: As the deployment of BBR increases, the harm should be relative to the amount of CUBIC in the system.
* **Ranysha**: You can play with the numbers; like this number does not matter much because there is very little CUBIC. 

## Extending Low Latency Service Across the Internet

* Speaker: **Fatih Berkay Sarpkaya**
* [Paper](https://arxiv.org/abs/2608.26601)
* [Slides](https://datatracker.ietf.org/meeting/127/materials/slides-127-iccrg-extending-low-latency-service-across-the-internet-00)

* **Lars Eggert**: It looks like we need to change the entire path for L4S to work; I wonder if that destroys a bunch of attractiveness of L4S. Do we need to do this to maximize the benefits or is it no longer enough to know where the bottleneck is, and just put L4S there?
* **Fatih**: The point is that we should do something for the upstream links also. 

* **Vidhi Goel**: Are these experiments performed on an actual deployed network?
* **Fatih**: Experiments have been performed in a controlled emulation, not an actual network.

* **Esteban Carisimo**: Is the assumption here that the bottleneck is neither in the access network nor at the content provider? How often does that happen?
* **Fatih**: Don't know the exact numbers of how upstream bottlenecks affect the L4S performance, but we just observed that it could still happen.

* **Esteban Carisimo**: A follow-up. You are propagating information through BGP, what is the cadence of those updates?
* **Fatih**: We haven't deeply tested this yet, but we need some coordination between domains to inform whether I support L4S or not. As for future work, we can study how practical this is.

* **Martin Duke**: Are the plots on Slide 8 telling that L4S makes the problem worse?
* **Fatih**: No, it tells that the other bottlenecks make the performance of L4S worse.

## Measuring Service Congestion, Sharing, and Pacing in a Residential Access Network

* Speaker: **Bruce Spang**
* [Paper](https://dl.acm.org/doi/pdf/10.1145/3777912.3839796)
* [Slides](https://datatracker.ietf.org/meeting/127/materials/slides-127-iccrg-measuring-service-congestion-sharing-and-pacing-in-a-residential-access-network-00)

* **Lars Eggert**: Slide 14, does it mean that the other flows saw the congestion but you didn't? So did you cause it?
* **Bruce**: I think no, but we will get to it.

* **Antonio Vicente**: About the games, are they interactive or download?
* **Bruce**: Like a file download.

* **Dave Seddon**: How are setting or unsetting the pacing? Youtube is always pacing.
* **Bruce**: This is not a transport layer pacing, this is the application is requesting a specific rate, and transport layer is spacing our packets to not send it faster than that rate

* **Vidhi Goel**: How did you do it for Youtube?
* **Bruce**: The collaborators from Youtube did it. And at Netflix, we turned it on.

* **Esteban Carisimo**: There is a lot of seasonality in academia, so one week may be completely different than the other. How did you remove this seasonality?
* **Bruce** Students were on the campus and did not leave half way through the experiment; more details are in the paper.
* **Esteban Carisimo**: A follow up. How can you relate this to any other environment?
* **Bruce** Was surprised to see congestion in this network; interested to see in other networks but this is what he had access to.

* **Martin Duke**: Did you specifically look at TCP flows?
* **Bruce**: Yes.
* **Martin Duke**: Did you have a metric running on the network side to see if it added to stalling
* **Bruce**: Details in the Sammy paper. A/B tests showed improvements in light retransmissions and RTTs without any impact on video

* **Kevin Fall**: Did you have any other signals like ECN? Was it IPv4 TCP?
* **Bruce**: Not sure, but it was probably IPv4. We did not look at ECN.

* **Vidhi Goel**: Did you collect the application metrics? 
* **Bruce**: In the data set, we did not. On the Netflix side, we did. But not captured in the paper because there was no improvement observed. 

* **Apoorv Kothari**: Which algorithm were you using?
* **Bruce**: Closer to what we published in the Samy paper; constants might be slightly different. 

* **Apoorv Kothari**: Was the overlap measured at the collector? overlap between services?
* **Bruce**: Yes, but for a very short time scale (just the packet level). Paper has details for an extended period of an hour.

* **Apoorv Kothari**: What's the purpose of measuring the access RTT?
* **Bruce**: We wanted a proxy for queuing delay, as a metric of congestion.

## TCP Segmentation Offload Without Microbursts: Splitting Pacing Between Host and NIC

* Speaker: **Sebastian Rust**
* [Slides](https://datatracker.ietf.org/meeting/127/materials/slides-127-iccrg-tcp-segmentation-offload-without-microbursts-01)

* **Lars Eggert**: I want to pace QUIC, any thoughts on that? The other question on how moongen applies a trick to make the NIC pace without all the machinery. I wonder whether that's the work that's possible with other NICs.
* **Sebastian**: Interested to work on pacing in QUIC. For the other question -- I believe they used DPDK; direct access to the NIC.  

* **Vidhi Goel**: Did you implement the timing wheel in the firmware? and what does the NIC provide? Is it a special NIC or is it something that every NIC can do?
* **Sebastian**: Yes. We implemented it in AKiTiO(?) because it had open-source firmware. It does require updating the firmware on the NIC, which may not be open-source always.  

* **Reese Enghardt**: Is there a scalability limitation if you have a lot of different flows and a lot of pace rates?
* **Sebastian**: The worst thing you will see is collisions, especially if you have an unfortunate pacing timing between 2 flows. For that, we overprovision the time wheel.
