---
title: DevOps — In a Nutshell
description: >-
    The most powerful tool we have as developers is automation.
date: '2018-10-03T16:32:16.722Z'
categories: ["DevOps"]
keywords: []
slug: /@itsmesunil/devops-in-a-nutshell-fa0988132de7
---

**“The most powerful tool we have as developers is automation**“.

Automation has become a buzzword in every organization and is followed in all the phases of software development until we have developed a successful product. Is our job completed after developing a successful product and releasing it to the customer? Not really, there is a continuous cycle of enhancement, fine-tuning, feedback loop. Is it good to have a continuous process to handle the new features or enhancements? That’s where the DevOps practice comes into play.

DevOps process answers the question like _how do I get a new feature, a new idea or an enhancement request quickly to production so that I can receive feedback as quickly as possible_ when it gets to the end users. The feedback is used to improve

> Efficiency and Performance

> Any enhancements to the shipped software

For faster shipping of code, a stable delivery pipeline is essential. So, **what exactly is a DevOps pipeline?**

It’s a setup in your software project that helps to deliver CI/CD in any organization. The idea is to create a pipeline which has _repeatable, stable and continuously improving_ process in order to make software delivery successful. A typical _Software Development Life Cycle_ is shown below:

![](/img/1__kC3dETA__QndHjFGTOMibyw.png)

A typical _DevOps Software Development Life-Cycle_ is shown below:

![](/img/1__jevTzpCIc__HPL__Y__KgbnWQ.png)

*   The developer writes code and checks into distributed code versioning system like Git/Bitbucket
*   The check-in of code triggers the build in the CI server
*   The CI server creates deploy-able artefacts for testing (EAR, WAR, JAR, Docker images, binaries ) for testing
*   Unit tests, Functional tests and System tests are done on the new build and issues are reported
*   Security and penetration testing are done on Production ready model.
*   Continuous Integration can also help to set up your production environment
*   If the build or tests fail, the CI server alerts the team through, Slack channels, Hip Chat, Email

Talking more on **Continuous Integration;** it is a development practice where developers push their code into a shared repository multiple times a day.

### Continuous Testing

Before moving into, continuous deployment, let’s start with understanding the difference between **Automation testing** and **Continuous testing**?

*   The process of automating the execution of test cases is called **Automation Testing**
*   Scheduling automated tests after every update of code is called **Continuous Testing.** The tests are continuously automated

The idea behind continuous testing in DevOps is to:

> _Get immediate feedback_

> _Validate functionality_

> _Find bugs early in the phase_

Another idea behind continuous testing is that you do not automate everything, automate only important tests/useful tests, automate tests that can find bugs. Do try to automate what fits the bill. There is should be a selection of tests that should be automated and then we measure coverage out of that be it user story coverage or requirements coverage.

Continuous testing is incorporated as part of the pipeline to obtain feedback on the risks associated with the product as quickly as possible. Most of the work is done by an automated test technique. Some of the strategies are:

*   Continuous testing is not about running your regression suite or any other suite over and over again. It about quality at every step, you do a build you test it, you change your environment you test it.
*   Continuous testing is the process of executing automated tests at the right stage of the pipeline

> _Test early, test often_ strategy

> Have fast, low-level tests that runs for every build

> Have moderate amount of tests that may occur only at integration or systems level

*   Continuous testing delivers actionable feedback at every stage of the pipeline
*   Continuous testing encircles the _Shift left (Unit testing, Code coverage, Integration testing)_ part and also the _Shift right part (Monitoring your apps )_
*   Continuous testing also must validate functional and non-functional requirements(Performance, Stability, Security). For example, if testing an API, the NFR’s could be :

> check the latency, average response time and should be reported back to the developer in the form of html output or some metric to do additional performance improvements,if needed

#### Continuous Delivery and Continuous Deployment

Continuous delivery is the capability to deploy the software to any given environment at a given point of time. This can be UAT, staging or production. We are constantly delivering the code to a user base for continual verification and validation.

We can see that until the deployment to Production, the pipeline is completely automated. The objective is to perform push-button deployments of any version of the software to any environment on demand.

**Continuous Delivery** is often conflicted with **Continuous Deployment**. Most of the born on the web companies do use this process. With continuous delivery, every code change made is built, had gone through the static code analysis and then tested and pushed to the non-production environment. From this stage, there would be parallel automation testing happening before declaring a GO for a manual approval for a push to the production environment.

**Continuous deployment** takes care that every change is traversed through the pipeline and promoted to production automatically. This will help in having many productions deployments every day.

**Assembly Lines — The next wave of DevOps**

Things around us always evolve and it’s in the IT world, this evolution is faster. One term rising in the DevOps world is Assembly Lines. This similar to car assembly lines, where different pieces of car (engines, axles ) comes together from different plants and merge to one assembly line.

Today, most organisations use various tools for automating specific DevOps activities. However, the DevOps toolchain is fragmented and gluing it together to achieve continuous delivery is a challenging task. Use of various tool have created islands of automation and assembly lines is all about connecting these islands of automation.

Group of pipelines merge together and form a single pipeline which deliver the final application.

For more info on Assembly lines:

[**What DevOps trends to follow (and what to ignore)**  
_You're dizzied by hours of researching DevOps trends and hashing it out with colleagues as you look towards what's…_lab.wallarm.com](https://lab.wallarm.com/what-devops-trends-to-follow-and-what-to-ignore/ "https://lab.wallarm.com/what-devops-trends-to-follow-and-what-to-ignore/")[](https://lab.wallarm.com/what-devops-trends-to-follow-and-what-to-ignore/)

[https://apifriends.com/digital-strategy/devops-pipeline/](https://apifriends.com/digital-strategy/devops-pipeline/)

Please do buzz me for any comment. Being a learner like all of you will try to assist in a humble way.