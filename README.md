This repository contains my Master's research project on improving elasticity in Apache Storm.

Apache Storm doesn't adapt well when running across heterogeneous nodes with data rates that change over time, which leads to CPU and bandwidth bottlenecks and rising latency. I designed and built an additional layer on top of Storm that gives it elasticity — the ability to detect and resolve these bottlenecks automatically, without manual intervention or restarting the system.

The solution works through two complementary mechanisms. Global adaptation monitors the system as a whole and decides when to create new replicas, where to place them, and when to safely remove underused ones without hurting throughput. Local adaptation works at the operator level, distributing load across downstream replicas based on real-time resource availability, so busy operators aren't overloaded further in the first place.

The full system was implemented and deployed on Docker across a cluster of heterogeneous nodes. Experimental results showed the system could create and remove replicas on the fly without interrupting execution, successfully detected and resolved CPU and bandwidth bottlenecks in real time, and scaled reliably

The implementation is split across four repositories:

storm-streaming-engine — contains the Storm pipeline itself and the local adaptation logic (operator-level load balancing).
DSP-orchestrator — contains the global adaptation service that monitors the cluster and makes scaling decisions.
elastic-distibuted-storm-deployment — contains the Docker Swarm deployment setup and the network simulation used to run experiments.
DSP-results-visualization — contains the Python scripts used to analyze and plot the experimental results.


