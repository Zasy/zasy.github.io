---
title: 'Optical Noc Thermal Aware Power Model'
date: 2018-08-15 11:44:02
tags: Noc
---
To the research of thermal-aware routing algorithm for optical NoC，a traffic-thermal co-simulation platform is necessary. The traditional optical NoC simulator gets the temperature distribution at first , then simulates the thermal-aware traffic activities. But more NoC simulators adopts the traffic-thermal co-simulation platform which is proposed by **Shang et al.[5].** Traffic-thermal co-simulation network platform for NoC integrated the traffic of network, power model and thermal model. During the simulation, the NoC simulator do traffic activities with the adaptive routing algorithm. The power model generate the power consumption based on the traffic activites, which is a power trace file. Thermal model gets the power trace infoomation. The thermal model updates temprature dsitributions with the given power trace file.   So the thermal-aware adaptive routing algorithm adjust the network traffic based on the newer temprature distributions of the optical NoC system.

We proposed a traffic-thermal co-simulation platform for the research of thermal-aware routing algorithm for optical NoC.



## A Traffic-thermal Co-simulation platform 

The proposed traffic-thermal co-simulaiton platform mainly consist of three parts: the optical network model, the learning based routing model and traffic-thermal co-simulation model. The optical network model is a SystemC-based cycle-accurate network simulator for optical NoC. The learning based routing model is the adaptive routing algorithm we proposed. We also implement a thraffic-thermal co-simulation platform for our optical NoC model. In our proposed work **before[],** we have introduced the optical network model  in detail. So in this section, we will first breify introduce the structure of the learning based routing model which is adopted in the router of network. Then we will describe the structure of traffic-therml co-simulation platform.

1. The structrue of learning based rouitng model

   We integrate the learning-based routing model in our optical NoC. When router model receive loss packets from other nodes, L-value calculator will caculate loss value based on the input loss packet and the optical thermal model. Then L-value update the corresponding the L-value in the L-Table as the algorithm which has been proposed in **Section 3**. When data packets is received from other nodes or processor, the Arbiter Unit will decide which port the packet go to as the input port and values in the L-Table. The arbiter unit will also send the loss packet at the same time. The whole strctrue of learning based routing model show as **Figure[].**

2. The structrue of traffic-thermal co-simulation model

   The traditional simulation model computes steady temperatures in HotSpot with the power trace hased been produced before, then simulate traffic activities in the optical network model with the steady temperatures. The problem of  traditioanl simulation is that the network simulator cannot update the tempeture distribution during the network simulation. Therefore, traditional simulation is unused for verifying thermal-aware designs for optical  NoC. A traffic-thermal co-simulation model is more suitable for verifying thermal-aware design. The whole traffic-thermal co-simulaiton model we proposed is showed as **Figure[]**. The optical NoC network simulator computes a period of traffic and transfer the power trace to the tempature model. The power trace is produced by the power model of the network. Then temprature model of Hotspot update the temprature distribution of the network with the power trace. The whole co-simulaton platform forms a loop between optical network and Hotspot temperature simulation. So the co-simualtion update the temperature distribution during the network simulation. It is necessary for the research of thermal-aware designs for optical NoC. 
