---
title: "Load Balancing in 5 Min."
datePublished: Wed Mar 15 2023 08:03:40 GMT+0000 (Coordinated Universal Time)
cuid: clf9ebcpq000209l0hm1f913c
slug: load-balancing-in-5-min
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1678866532105/d4055e74-1fb3-4b9e-aab3-88e639351a0d.png
tags: load-balancer, hashing, load-balancing, learning-in-public, wemakedevs

---

[LoadBalancing image](https://www.nginx.com/wp-content/uploads/2014/07/what-is-load-balancing-diagram-NGINX-640x324.png)

Let's say there is an algorithm running on the server.

<details data-node-type="hn-details-summary"><summary>What is Server?</summary><div data-type="detailsContent">A <a target="_blank" rel="noopener noreferrer nofollow" href="https://www.simplilearn.com/what-is-a-cloud-server-article" style="pointer-events: none">Server</a> is which servers the request.</div></details>

* When a person is connecting through a mobile/PC to a server, they are technically sending a request. Then the algorithm runs and then the response is sent back. Let's say there are thousands and thousands of requests coming. Your server cannot handle this anymore. So what you do is add another server. If we do this, there's one problem i.e where do you send the requests? for example: If there is a person, then which server should the person send a request to?
    
* In general, when we have 'N' servers, then we need to balance the load on all the servers. The servers have **Load** on them. And the concept of actually taking 'N' servers and trying to balance the load evenly on all of them is called ***Load Balancing***.
    
* What we are going to do is take these requests and evenly balance the load on all of our 'N' servers and the concept of **Consistent Hashing** will help us do that. (*<mark>We will learn more about Consistent Hashing in the next blog, now we will learn about normal hashing</mark>*).
    
* So you will evenly distribute the weight across all servers. You will get a request ID in each request and will be uniformly random.
    
    Example:
    
    request 1 ---&gt; (r1)
    
    Now, we will perform hashing and get a particular number m1.
    
    Example:
    
    h(r1) ---&gt; m1 ---&gt; (Equation-1)
    
    This number (m1) can be mapped to a particular server by:-
    
    m1 % n ---&gt; (Equation-2)
    
    (where 'n' is the number of servers)
    
    And then we will get an index and send it to the respective server.
    
* Let's say we have 4 servers (S0, S1, S2, S3). By performing hashing to the request ID and based on the output, we will send the request to a particular server.
    
    * h(10) ---&gt; 3 % 4 (Using Equation-1 & 2)
        
        r1 = 3. (Request(r1) is directed to S3).
        
    * h(20) ---&gt; 15 % 4 (Using Equation-1 & 2)
        
        r2 = 3. (Request(r2) is directed to S3).
        
    * h(35) ---&gt; 12 % 4 (Using Equation-1 & 2)
        
        r3 = 0. (Request(r3) is directed to S0).
        
* In general, because this is uniformly random and our hashing function is uniformly random, we can expect all the servers to have a uniform load.
    
    Each of the servers which have 'X' requests will have (X/n) load, Where 'n' is the number of servers.
    
    Load Function = 1/n.
    
* Here, everything seems to work fine, except what happens if you add more servers.
    
* There will be problems arising with adding and removing servers. Here the requests which are being served are entirely puzzled.
    
* Previously in the hash Function, we have to do
    
    h(10) ---&gt; 15 % 4= 3
    
    and this request (r1) is directed to S3. But with more servers, we have to make some changes i.e change the value of 'n' from 4 to 5.
    
    h(10) ---&gt; 15 % 5 = 0
    
    and this request (r1) will be directed to S0.
    
    Just like this, every request will change i.e 100% of the request will change.
    

**So you might think what's the problem?**

* Because in practice the request ID is never random or it's rarely random.
    
* The request ID encapsulates some of the information of the user. Example: userID.
    
    Let's understand it by an example:-
    
* * If we hash "Priyansu" this hash is going to give the same result again and again, cause the hash function is constant. And it will lead to the same server again and again. Then why not use the information if we are sent to the same server regularly? And if there is something like fetching a profile from a database why should we do that all the time, why not store it in the local cache?
        
        * So depending on the user ID, we can send people to a specific server and once they are sent there you can store relevant information in the cache for those servers.
            
        * Now that's the case. But as we add more servers the policy changes and the entire system changes and all users are now randomly sent to different servers and all the useful cache information is dumped and is completely useless.
            
        * So, what we want is to avoid huge changes in the range of the number we are serving. So what we want is a tiny change such that the sum of the changes is going to be 20%.
            
            ![](https://cdn.hashnode.com/res/hashnode/image/upload/v1678866126768/4dbfc739-b6b6-48da-af14-fbc378b0cd4d.png align="center")
            
        * The overall changes should be minimum, that's the general idea of why the old hashing doesn't work in this case. So, we need more advanced approaches and that's where ***consistent hashing*** comes in. *<mark>(We will learn more about Consistent Hashing in the next blog).</mark>*
            

If you guys have any suggestions, feel free to contact me on

**priyansusahoo1@gmail.com**