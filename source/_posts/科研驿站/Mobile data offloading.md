---
title: Cellular Traffic Offloading
date: 2014-09-28
tags:
- paper
- mobile data offloading
categories:
- 科研驿站
---
  
*Reference:*  
**[1] Mobile Data Offload for 3G Networks**  
**[2] Mobile Data Offloading through Opportunistic Communications and Social Participation**  
**[3] Femtocell Networks: A Survey**  

There are two types of existing solutions to alleviate the traffic load on cellular networks: offloading to femtocells and WiFi networks.  
<!-- more -->  
### 1. Femtocell for Indoor Environments
Originally, the femtocell technology (i.e., access point base stations) was proposed to offer better indoor voice and data services of cellular networks. Femtocells work on the same licensed spectrum as the macrocells of cellular networks and thus do not require special hardware support on mobile phones. But customers may need to install short range base stations in residential or small-business environment, for which they will provide Internet connections. Due to their small cell size, femtocells can lower transmission power and achieve higher signal-to-interference-plus-noise ratio (SINR), thus reducing the energy consumption of mobile phones. Cellular operators can reduce the traffic on their core networks when indoor users switch from macrocells to femtocells. A literature review about the technical details and challenges of femtocells can be found in Chandrasekhar et al.[3]  

### 2.Cellular Traffic Offloading to WiFi Networks
Compared to femtocells, WiFi networks work on the unlicensed frequency bands and thus cause no interference with 3G cellular networks. As a result, cellular network operators, including AT&T, T-Mobile, Vodafone, and Orange, have deployed or acquired WiFi networks worldwide [1]. Meanwhile, there are already several offloading solutions and applications proposed from the industry. For instance, the Line2 iPhone application (available at http://www.line2.com) clones the phone’s own software and can initiate voice calls over WiFi networks. iPassConnect enables end users to switch between 3G cellular and WiFi connections smoothly, and provides them a one-touch login for more than 100,000 hotspots operated by 100þ providers. Recently, Balasubramanian et al. have proposed a scheme called Wiffler to augment mobile 3G networks using WiFi for delay-tolerant applications.

Offloading cellular traffic to femtocells and WiFi networks is limited by their network deployment and relies on the availability of Internet access. Instead, we offload mobile data traffic through opportunistic communications for information dissemination, in metropolitan areas.