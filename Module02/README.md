# Module 2

> **Example module** from the IoT introduction class. Adjust the headings and tasks to match your actual course content.

We are going to show here notes for Task 1, 2, 3, 4, and 5 to prove

## Learning Goals

> **How to use the learning goals.** Copy the module's learning goals from the course workbook into the block below. Keep the `LG1`, `LG2`, … IDs and a one-word keyword. In each task, write `Proves: LG2` (or link to `[LG2](#lg2)`) so you can find the evidence quickly at checkpoint time. In the **Evidence** line under each goal, link to the task that proves it.

## Learning Goals

<a id="lg1"></a>
### LG1 — `<IP-config>`

<Configure IPv4 addressing, CIDR subnetting, default gateways, and routing tables.>
[rein2max@DIVA OpenWRT auf Cudy einrichten]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: wlo1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether d0:3c:1f:0e:6a:4b brd ff:ff:ff:ff:ff:ff
    altname wlp3s0
    altname wlxd03c1f0e6a4b
    inet 192.168.14.103/24 brd 192.168.14.255 scope global dynamic noprefixroute wlo1
       valid_lft 43195sec preferred_lft 43195sec
    inet6 fd6e:2ff7:e75b::257/128 scope global dynamic noprefixroute 
       valid_lft 43194sec preferred_lft 43194sec
    inet6 fd6e:2ff7:e75b:0:a590:93fa:1013:de38/64 scope global dynamic noprefixroute 
       valid_lft 5394sec preferred_lft 2694sec
    inet6 fe80::d7c3:9c8:8cd:f092/64 scope link noprefixroute 
       valid_lft forever preferred_lft forever


**Evidence:** [Task 1](#task-1)

<a id="lg2"></a>
### LG2 — `<IP-plumbing-services>`

<Inspect and diagnose the core IP plumbing services: ARP, DHCP (DORA), DNS, and NAT.>

> We have successfully done our ssh configuration

**Evidence:** [./pictures/Dfhoverlay.jpg](#task-2)

<a id="lg3"></a>
### LG3 — `<routing>`

<Flash, configure, administer, and secure an OpenWrt edge router via SSH and the LuCI web interface — from factory firmware to a working pod LAN with a WAN uplink (eduroam, phone tether, or the class Wi-Fi).>

> We have successfully configured the router

**Evidence:** [Task 3](#task-3)

<a id="lg4"></a>
### LG4 - `<capture-traffic>`

<Capture traffic at the choke point with tcpdump on the router, and read the dump with Wireshark, tshark, or as text — without needing a second network adapter.

> We have successfully done it, proof is shown via the screenshot: <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ab29c13f-2017-4b63-a08f-684ca837d8cc" />



### Pre-study-check-in
have to add 1 question i still have

## Network plan — the sketch, the subnet calculation, the SSID/channel, and the pod ID.

## Router baseline — model, OpenWrt version, LAN/WAN addresses, MACs, SSH access, extroot status, broker status, open ports. No passwords, no eduroam credentials.

## Study log — the running log: the theory you actually needed, the commands that surprised you, and the LLM answers you checked. This is not an essay and not a separate study phase.
We 

## Discussion log — one line per discussion: who listened, what they asked, what you changed. This is personal; the shared study log is still one per pod.

## Vocabulary tracker — the Module 2 vocabulary table, copied with two extra columns: ✓ and Link / evidence. See the reference at the end for how to fill it.

## Captures — the pcap or the tshark/tcpdump -A text, and what each protocol proves.

## NAT and port forwarding — the rule, the two-sided capture, and the explanation.

## Take it home — the upstream switch and the evidence that the router still works.

## Story seeds — optional: the odd bits worth turning into a story later.

**Evidence:** [Task 3](#task-3)

<a id="task-1"></a>
## Task 1 — `<short title>`

**Proves:** [LG1](#lg1)

This task was executed by myself.

<a id="task-2"></a>
## Task 2 — `<short title>`

**Proves:** [LG2](#lg2)

This task was executed by my partner. The implementation was about ...
It is [here](https://github.com/partner/iot-portfolio/Module02/README.md#task-2).

<a id="task-3"></a>
## Task 3 — `<short title>`

**Proves:** [LG3](#lg3)

## Round 1:

## Round 2:

## Round 3:

## Round 4:

## Round 5:

## Round 6:

## Round 7:

## Round 8:

## Round 9:
1. Release Story: "OpenWrt ​is a highly extensible ​GNU/​Linux ​distribution for embedded devices ​(typically wireless routers). Unlike many other distributions for these routers, OpenWrt ​is built from the ground up to be a full-featured, easily modifiable operating system for your router. In practice, this means that you can have all the features you need with none of the bloat, powered by a Linux kernel ​that's more recent than most other distributions."



...

## Reflection 2

[Reflection 2](../Reflections/ref02.md)

If the module is longer than 1 week, you might have several reflections within it. If not, delete this and the following.

## Reflection 3
[Reflection 3](../Reflections/ref03.md)
