---
title: "Horizontal & Vertical Scaling in 5min"
datePublished: Thu Mar 09 2023 13:47:46 GMT+0000 (Coordinated Universal Time)
cuid: clf15yqq0000109lg9e9cfmvq
slug: horizontal-vertical-scaling-in-5min
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678367668718/fd8d9a2b-18c4-4969-828d-80bbae6a9adc.jpeg
tags: cloud-computing, learning-in-public, horizontal-scaling, vertical-scaling, wemakedevs

---

* Guess the code that we have running on the server is not able to handle all of these connections.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678366785527/75a2d5af-14b7-48b4-ae3e-ced7be99e697.png align="center")

* So to handle all the connections, we can:
    
    1. BUY BIGGER MACHINES, OR
        
    2. BUY MORE MACHINES.
        

And the ability to handle more requests by buying more Machines is ***HORIZONTAL*** Scaling & buying bigger machines is ***VERTICAL*** Scaling.

### Horizontal Vs Vertical Scaling

| Horizontal Scaling | Vertical Scaling |
| --- | --- |
| \- Load Balancing required. | \- N/A, cause as we have a single machine, so there's no load as such to balance. |
| \- With lots of machines, if one of the machine fails, you can redirect the requests to other ones. (RESILIENT) | \- N/A, Single point failure. |
| \- Communication that we have between the servers will be over the network and the network is also slow i.e it's I/O. | \- Here we have interprocess communication. So that is quite fast. |
| \- **DATA INCONSISTENCY.** E.g:- Let's say we are having a transaction, where different machines send data to one another. Here we see that data is complicated to maintain. If there is a transaction where the operation has to be atomic, what could happen is that we have to lock all the servers i.e the databases, which is impractical. So usually what happens is we have some sort of loose transactional guarantee. | \- **CONSISTENCE**. Here there's just one system on which all the data resides and that's why it's consistent. |
| \- Scales well as users increase. | \- Has a hardware limit. |

### So, the question is which type of scaling is used in the real world?

* The answer is **Both**. We take some good qualities of vertical scaling which is really fast interprocess communication and the data being consistent.
    
* And some good quality from horizontal scaling i.e it scales well and is also resilient i.e if one machine fails then the request is redirected to another machine.
    
* The Hybrid solution is horizontal scaling where each machine has a big box i.e each machine you try to take as bigger as possible as feasible money-wise and we pick up a solution this way.
    

If you guys have any suggestions, feel free to mail me on

**priyansusahoo1@gmail.com**