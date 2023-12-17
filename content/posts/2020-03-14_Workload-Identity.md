---
title: Workload Identity — A SPIFFE Primer
description: >-
  Spiffe security framework
date: '2020-03-14T09:37:54.769Z'
categories: ["tech", "security"]
keywords: []
slug: /@itsmesunil/workload-identity-a-spiffe-primer-533d79f4e53a
draft: true
---

![](/img/lock.jpg)

Applications are being broken down from monolith to microservices and are mainly deployed on cloud platforms. Environments, where we deploy our microservices, needs to be protected from outside threats. Cloud-native microservice applications are secured using certificates, real-time threat monitoring etc. When nodes are dynamically scaled, the challenge is how can we bootstrap trust between newly scaled nodes and the existing ones. Here comes the problem of **workload identity**.

> A workload is an **application or a service** deployed on the cloud. It can be a webserver, a container or a node

Firewall security is coarse-grained (one level of access to data). In classical security models, IP address is the identity available to the network. What happens to your IP address identity in vibrant environments like Kubernetes where IP addresses change for workloads over time.

Cloud platforms use security groups, instances use IP whitelisting to secure. This outer wall helps to stop the attacks, but once it is breached, the wrong guy may get access to our systems.

Am running on someone else’s network and my systems are much more elastic or dynamically scaled. The challenge of having an identity, rotating secrets and automated bootstrap for trust and make it available for other systems to authenticate is something that has to be answered.

SPIFFE (**S**ecure **P**roduction **I**dentity **F**ramework **f**or **E**veryone) helps to address the problem of workload identity.

All of us carry an identity and also when we interact with systems we do have some identity to start with. When we want to log into our email account, we do know our Username and also do know the password which is some form of identity. This identity is carried around with us almost all the times. In essence, this is what SPIFFE does to workloads which can be your VM’s, containers, applications etc.

SPIFFE helps parts of a distributed system to trust each other, which run in dynamic and heterogeneous environments. SPIFFE is an open standard that defines a way that a microservice (a workload in SPIFFE terminology) can establish identity. SPIFFE Runtime Environment (SPIRE) is an open-source reference implementation of SPIFFE. An analogy which can be thought of the credit card we hold. They are issued by different banks but do have similar characteristics, similar to SPIFFE specifications. They have the same size, they have a 16 digit card number. When the card is used at the POS terminal or ATM it can be read. SPIRE is the card-issuing agency here.

SPIRE implements the card specifications ( SPIFFE ) and enables for all machines ( workloads ) as they scale up. This is what SPIFFE does. It does bootstrap and issue identities. SPIFFE is:

*   A standard defining how services identify themselves to each other. These are called **_SPIFFE IDs_** and are implemented as [Uniform Resource Identifiers (URIs)](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier).
*   A standard for encoding SPIFFE IDs in a cryptographically-verifiable document called a **SPIFFE Verifiable Identity Document or _SVIDs_**.a URI Subject Alternative Name can be added to a typical x509 certificate to provide a service with a unique identity.
*   An API specification for issuing and/or retrieving SVIDs. This is the **_Workload API_**.

> Source: [https://github.com/spiffe/spiffe#communications](https://github.com/spiffe/spiffe#communications)

The service identity is encoded in URI with the scheme spiffe, for eg: **spiffe://trust-domain/path/to/workload**

The trust-domain is specifically the host section of the authority. The path section can be UUID, while in Kubernetes the path is a combination of service account name and namespace as shown below.

![](/img/mtls.png)

### The working:

The two main components are the SPIRE Server and SPIRE agent. The agent runs on the same node where the workload is running.

1.  Node Attestation: Verify the identity of the node the workload is running on. Attestation is the process of certifying something is true

For the workload running on Kubernetes environment, the node agent uses the token given by Kubernetes cluster to prove its identity to the SPIRE server. This token uniquely identifies the node.

2\. SPIFFE ID’s are issued by the server, with a set of selectors. Selector associate a SPIFFE ID to a node

![](/img/spiffe.png)

The above process is called as node attestation. All this information is stored in a registry entry

3\. After the node is identified, the workload has to be identified. When a workload starts running on a node, it asks the workload API “who am I?”

![](/img/workload_attestation.png)

4\. The SPIFFE node agent receives the request from the workload. The agent tries to identify the PID related to the workload, creates a Certificate Signing Request (CSR), and sends the CSR to the SPIRE server

![](/img/svid.png)

5\. The server responds to the node agent with the signed SVID for the workload along with the trust bundles, indicating which other loads can be trusted by this workload

The issued SVID’s (can be an X.509 certificate) are ephemeral; they expire in an hour. The benefit of short-run certificates are attacks are bounded within that time, if any.

The SVID has:

*   SPIFFE ID
*   A public key that represents the workload
*   Valid signature

6\. The node agent then passes the signed certificate (SVID) and corresponding private key to the workload and the trust bundles. The workload can now talk to other workloads over mTLS.

An overview of workload attestation is shown below:

![](/img/spire.png)

To conclude, SPIFFE provides end-to-end automatic encryption and mutual authentication between services. There are a lot of use cases with open-source SPIFFE and SPIRE projects. Our environments should be secure in a seamless way and SPIFFE gives that.

Please feel free to put thoughts or comments [Sunil Jacob](https://medium.com/u/7d5c1c8a35bd).