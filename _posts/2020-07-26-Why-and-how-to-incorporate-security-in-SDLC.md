---
layout: post
title: Why and how to incorporate security in SDLC
date: 2020-07-26 07:57
category: SDLC
author: vivek.srivastava
tags: ["Security", "SDLC", "Development", "Testing"]
comments: true

summary: Due to the large number of attacks that are occuring today, it is of paramount importance that software be built securely. Analyzing the risk from the initial phases of the development life cycle will not only make the product secure from current attacks but also help plan and mitigate risks arising out of future attacks. A software developed without security considerations, is secured by doing patchwork, and finally one realises that the bandwidth regired to secure the software is too high, thus resulting in very high costs.

feature_img: /images/post_images/images-blog-qac-secure-software-development.jpg
medium: 
linkedin:
facebook:
twitter:
youtubeId:
excerpt_separator: <!--more-->
---

# Importance of Security in the SDLC

Software Development Lifecycle (SDLC) is a process followed to develop a software product.
 
Keeping security in mind during every stage of the SDLC is extremely vital to keep the software product immune from any future cyber-attacks. This is also referred to as baking the security into your software development.
 
Following the SDLC security practices provide risk exposure for your product. Well immunity may be over-the-board but detection and minimizing the risks is an important factor. Keep in mind that you cannot defend your system against the risks that you don’t see. Thus, baking security in your product saves you time and money in the long run. It is also referred to as containing the risk or minimizing the risk in the future.
 
Similar to the Quality analysis of functional requirements, it is also important that we validate the security assessment as we go along the design, development of the product. If not it can get all the way to the end of the process only to then realize that there are security issue and the developed software is insecure.
 
Starting over at that point would set you back tremendously over time and money. Therefore, deciding whether or not to take appropriate security measures throughout the SDLC must not be a question.

# Incorporating Security In SDLC

Having established the importance of Security in SDLC, jets go over the phses of software development and how to make the product secure at each phase.

## Analysis Phase- Embed Security Requirements
 
Requirement analysis phase being the early phase of the SDLC, you must analyze the security requirements. Along with software’s functional/non-functional requirements, you must complete the threat analysis to identify potential risks ahead of time and gather requirements around it to address
them during design/development phases. While writing your functional requirements assess all the functional requirements from a threat perspective. Do any of the functional requirements create/pose any threat? If yes, review the functional requirement from the “must-have” / “nice to
have” perspective.
 
Performing the threat analysis is going to define the areas/requirements which pose risk to your software while giving you a better understanding of how to address them.
 
## Design, Development &amp; Testing Phase- Implement and Test Security
 
You must always design your software keeping security as the one important pillar. Follow secure coding best practices during the development phase, perform code review against security protocols implemented.
 
Throughout the coding process, implement checks and balances to review the security. Continually review the source code and run security testing before approval. Not to forget that the system and regression testing are very vital as these phases can discover loopholes that hackers exploit. Implement good controls, that meet regulatory compliance and security standards, and make sure you test that they are working as expected.

Another testing specific to security, Dynamic Application Security Testing (DAST), can be used to scan the software after they are implemented, and you must use the Static Application Testing (SAT) for code review.
 
## Security management while off sourcing Development
 
Most often companies leverage the third-party organizations to perform different phases of SDLC, e.g., Requirement analysis from one vendor and design and development via another vendor. 
 
Not all these vendors bake the security requirements or follow secure coding standards. Therefore, it is very important that you track the security aspect of your software in mind. Make sure that the developers are following secure coding best practices. If possible, have the security testing as contractual requirements when you outsource. It is always better to outsource the security testing to an independent organization that can make sure that security is baked into the software as per current industry standards.
 
 
## Post Deployment Maintenance

Once the software is deployed, as you monitor your system from day to day operations perspective, it is advised to monitor your software against the new threat landscape and perform vulnerability assessment periodically.
 
Post software deployment, oftentimes changes are added into the product making it susceptible to the security threat. If you bake security into your software, you will be able to identify changes quickly and enhance your system to avoid any future security threat.

