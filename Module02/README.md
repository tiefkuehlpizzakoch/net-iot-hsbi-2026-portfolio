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


<img width="1688" height="817" alt="image" src="https://github.com/user-attachments/assets/43bb59d3-8556-4143-957d-b590c5ace991" />

## Study Log

> During the router setup we have discovered, that it is not a good idea to flash the transition firmware twice, as it breaks the router configuration.

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
Downloaded the necessary firmware to be flashed onto the router. 

## Round 2:
We have successfully extended the routers storage using a USB flash drive, so that more packages can be installed. 

# Round 3

> We have successfully set up our connection to eduroam so that we can have an access to Wi-Fi.
> We can also connect to our private network according to the information found in module 2, Path C; Source: <a href="https://github.com/iotempire/iotempire-teaching/blob/main/full-classes/hsbi-networking-iot-10d/modules/02-local-networking-and-gateways.md">Module 2</a>

# Round 4

> We have successfully changed the network interface from 192.168.0.1 to 192.168.14.1/24 and tested the connection to the network interface WIRELESSLY

# Round 5

> Proves LG4: <a href="lg4">SOURCE</a>. We have also created a screenshot of tcpdump located at: ./pictures/tcpdump.png

# Round 6

> 1. /26 calculation
> 2^(32 - 26) = 2^6 = 64 - the total amount of addresses  <--
> Usable hosts: 64 - 2 (Network AND Broadcast) = 62         |
> Block size: 256 - 192 = 64                                |
> Network Address: 192.168.14.0                             |
> Broadcast: 192.168.14.63 --------Proves--------------------
> Usable range is naturally then from 192.168.14.1 to 192.168.14.62

> /28 calc is naturally then
> total 16; usable hosts 14; block size 16; network address at 0 broadcast at 15, and the range is from 1 to 14
> Our broker address however remains unchanged, hence it doesnt really matter if the subnet is /24 or /26 or /28


# Round 7

> The interaction could work if only I had a different client set up. The test screenshot can be found as tcpdump-interaction.png and the setup at the
> router interface and Konnichiwa.png. Yet I am connected to the private network and everything works fine.

# Round 8

> Our router works just fine at home - instead of setting up the connection to eduroam, it was connected to the private network as seen in some screenshots in previous rounds. 

> Here is an example of the prepared ssh:
[rein2max@DIVA ~]$ ssh root@192.168.14.1
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
root@192.168.14.1's password: 


BusyBox v1.37.0 (2026-11-05 11:43:20 UTC) built-in shell (ash)

  _______                     ________        __
 |       |.-----.-----.-----.|  |  |  |.----.|  |_
 |   -   ||  _  |  -__|     ||  |  |  ||   _||   _|
 |_______||   __|_____|__|__||________||__|  |____|
          |__| W I R E L E S S   F R E E D O M
 -----------------------------------------------------
 OpenWrt 25.12.6, r33311-981c978eff Dave's Guitar
 -----------------------------------------------------

 OpenWrt recently switched to the "apk" package manager!

 OPKG Command           APK Equivalent      Description
 ------------------------------------------------------------------
 opkg install <pkg>     apk add <pkg>       Install a package
 opkg remove <pkg>      apk del <pkg>       Remove a package
 opkg upgrade           apk upgrade         Upgrade all packages
 opkg files <pkg>       apk info -L <pkg>   List package contents
 opkg list-installed    apk info            List installed packages
 opkg update            apk update          Update package lists
 opkg search <pkg>      apk search <pkg>    Search for packages
 ------------------------------------------------------------------

For more information visit:
https://openwrt.org/docs/guide-user/additional-software/opkg-to-apk-cheatsheet

root@OpenWrt:~# ubus call system board
{
        "kernel": "6.12.112",
        "hostname": "OpenWrt",
        "system": "MediaTek MT7628AN ver:1 eco:2",
        "model": "Cudy TR1200 v1",
        "board_name": "cudy,tr1200-v1",
        "rootfs_type": "squashfs",
        "release": {
                "distribution": "OpenWrt",
                "version": "25.12.6",
                "firmware_url": "https://downloads.openwrt.org/",
                "revision": "r33311-981c978eff",
                "target": "ramips/mt76x8",
                "description": "OpenWrt 25.12.6 r33311-981c978eff",
                "builddate": "1792273538"
        }
}
root@OpenWrt:~# 192.168.14.1/26
-ash: 192.168.14.1/26: not found
root@OpenWrt:~# ip addr show
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc fq_codel state DOWN qlen 1000
    link/ether d4:0d:ab:52:a4:20 brd ff:ff:ff:ff:ff:ff
4: br-lan: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether d4:0d:ab:52:a4:20 brd ff:ff:ff:ff:ff:ff
    inet 192.168.14.1/26 brd 192.168.14.63 scope global br-lan
       valid_lft forever preferred_lft forever
    inet6 fd6e:2ff7:e75b::1/60 scope global noprefixroute 
       valid_lft forever preferred_lft forever
    inet6 fe80::d60d:abff:fe52:a420/64 scope link 
       valid_lft forever preferred_lft forever
5: eth0.1@eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue master br-lan state LOWERLAYERDOWN qlen 1000
    link/ether d4:0d:ab:52:a4:20 brd ff:ff:ff:ff:ff:ff
6: eth0.2@eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state LOWERLAYERDOWN qlen 1000
    link/ether d4:0d:ab:52:a4:20 brd ff:ff:ff:ff:ff:ff
7: phy0-ap0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master br-lan state UP qlen 1000
    link/ether d4:0d:ab:52:a4:20 brd ff:ff:ff:ff:ff:ff
11: phy1-sta0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether d4:0d:ab:52:a4:22 brd ff:ff:ff:ff:ff:ff
    inet 192.168.0.200/24 brd 192.168.0.255 scope global phy1-sta0
       valid_lft forever preferred_lft forever
    inet6 fe80::d60d:abff:fe52:a422/64 scope link 
       valid_lft forever preferred_lft forever
root@OpenWrt:~# ip link show br-lan
4: br-lan: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP qlen 1000
    link/ether d4:0d:ab:52:a4:20 brd ff:ff:ff:ff:ff:ff
root@OpenWrt:~# df -h
Filesystem                Size      Used Available Use% Mounted on
/dev/root                 7.0M      7.0M         0 100% /rom
tmpfs                    60.0M    300.0K     59.7M   0% /tmp
/dev/sda1                 7.2G      2.0M      6.8G   0% /overlay
overlayfs:/overlay        7.2G      2.0M      6.8G   0% /
tmpfs                   512.0K         0    512.0K   0% /dev
/dev/mtdblock6            6.7M    376.0K      6.3M   5% /rwm
root@OpenWrt:~# ss -tlnp
-ash: ss: not found
root@OpenWrt:~# date
Thu Nov 19 20:08:06 CET 2026

> We are successfully prepared for the next Module as everything seems to be in order

# Round 9

> 1. OpenWrt started in January 2004 from Linksys WRT54G GPL sources and expanded in 2005 with a custom buildroot2 system based on official GNU Linux kernel sources.
> The project exists to replace proprietary vendor code with free tools for flashing, wireless configuration, and VLAN control, giving users full ownership of their hardware.
> 2. Device: Cudy TR1200 v1. Supported release 25.12.2. Install method: TFTP only. DFS channels are not supported on the 5 Ghz MT7613 radio chip.



...

## Reflection 2

[Reflection 2](../Reflections/ref02.md)

If the module is longer than 1 week, you might have several reflections within it. If not, delete this and the following.

## Reflection 3
[Reflection 3](../Reflections/ref03.md)
