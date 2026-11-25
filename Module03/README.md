> Name: Julius Zünkeler
> Module 3: Nebula and OpenWRT setup. Overlay and mesh Networks

## Overlay Plan


## Study Log

# Task 1

> The bundle packages were received and installed on the router's storage via ssh, as well as luci-proto-nebula.

# Task 2

> Successfully connected to the pod LAN for our NodeRED:
> http://ulno-oldplex04.hsbi01.ulno.mesh:18080
> the proof can be found at: ./pictures/

# Task 4

> find at: ./pictures

# Task 5

> In order to test the overlay network, we first pinged it, then we tried the following command lines:
iperf3 -c 10.100.1.1 -t 10          # uplink
iperf3 -c 10.100.1.1 -t 10 -R       # downlink
iperf3 -c 10.100.1.1 -t 10 -P 4     # parallel streams

# LAN baseline, for comparison: run iperf3 -s on the router, then
iperf3 -c 192.168.14.1 -t 10

> The last one didn't work because we had to run iperf3 -s IN THE SEPARATE WINDOW. To clarify, we asked a foreign group member, Kelvin, and he told us, that the problem was that we tried to load everything in one terminal window. Since iperf3 -s is a different process, we had to open a separate window for the final command line to ping. The result was successful:
root@OpenWrt:~# iperf3 -c 192.168.14.1 -t 10
iperf3: error - unable to connect to server - server may have stopped running or use a different port, firewall issue, etc.: Connection refused
root@OpenWrt:~# iperf3 -c 10.100.1.1 -t 10
Connecting to host 10.100.1.1, port 5201
[  4] local 10.100.0.19 port 37334 connected to 10.100.1.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  4]   0.00-1.00   sec   384 KBytes  3.15 Mbits/sec    0   79.2 KBytes       
[  4]   1.00-2.00   sec   384 KBytes  3.14 Mbits/sec    0   97.5 KBytes       
[  4]   2.00-3.00   sec   512 KBytes  4.20 Mbits/sec    0    113 KBytes       
[  4]   3.00-4.00   sec   384 KBytes  3.14 Mbits/sec    0    132 KBytes       
[  4]   4.00-5.00   sec   384 KBytes  3.14 Mbits/sec    0    152 KBytes       
[  4]   5.00-6.00   sec   384 KBytes  3.14 Mbits/sec    0    173 KBytes       
[  4]   6.00-7.00   sec   512 KBytes  4.20 Mbits/sec    0    201 KBytes       
[  4]   7.00-8.00   sec   640 KBytes  5.24 Mbits/sec    0    258 KBytes       
[  4]   8.00-9.00   sec   256 KBytes  2.10 Mbits/sec    0    338 KBytes       
[  4]   9.00-10.00  sec   384 KBytes  3.14 Mbits/sec    0    434 KBytes       
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  4]   0.00-10.00  sec  4.12 MBytes  3.46 Mbits/sec    0            sender
[  4]   0.00-11.05  sec  4.00 MBytes  3.04 Mbits/sec                  receiver

iperf Done.
root@OpenWrt:~# ^C

root@OpenWrt:~# iperf3 -c 10.100.1.1 -t 10 -R
Connecting to host 10.100.1.1, port 5201
Reverse mode, remote host 10.100.1.1 is sending
[  4] local 10.100.0.19 port 42222 connected to 10.100.1.1 port 5201
[ ID] Interval           Transfer     Bitrate
[  4]   0.00-1.00   sec   384 KBytes  3.14 Mbits/sec                  
[  4]   1.00-2.00   sec   512 KBytes  4.19 Mbits/sec                  
[  4]   2.00-3.00   sec   384 KBytes  3.14 Mbits/sec                  
[  4]   3.00-4.00   sec   384 KBytes  3.15 Mbits/sec                  
[  4]   4.00-5.00   sec   512 KBytes  4.19 Mbits/sec                  
[  4]   5.00-6.00   sec   384 KBytes  3.15 Mbits/sec                  
[  4]   6.00-7.00   sec   512 KBytes  4.19 Mbits/sec                  
[  4]   7.00-8.00   sec   384 KBytes  3.15 Mbits/sec                  
[  4]   8.00-9.00   sec   512 KBytes  4.20 Mbits/sec                  
^C[  4]   9.00-9.54   sec   256 KBytes  3.87 Mbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  4]   0.00-9.54   sec  0.00 Bytes  0.00 bits/sec                  sender
[  4]   0.00-9.54   sec  4.12 MBytes  3.63 Mbits/sec                  receiver
iperf3: interrupt - the client has terminated by signal Interrupt(2)
root@OpenWrt:~# iperf3 -c 10.100.1.1 -t 10 -P 4 
Connecting to host 10.100.1.1, port 5201
[  4] local 10.100.0.19 port 39294 connected to 10.100.1.1 port 5201
[  6] local 10.100.0.19 port 39298 connected to 10.100.1.1 port 5201
[  8] local 10.100.0.19 port 39300 connected to 10.100.1.1 port 5201
[ 10] local 10.100.0.19 port 39308 connected to 10.100.1.1 port 5201
[ ID] Interval           Transfer     Bitrate         Retr  Cwnd
[  4]   0.00-1.00   sec   256 KBytes  2.10 Mbits/sec    0   37.8 KBytes       
[  6]   0.00-1.00   sec   128 KBytes  1.05 Mbits/sec    0   39.0 KBytes       
[  8]   0.00-1.00   sec   128 KBytes  1.05 Mbits/sec    0   39.0 KBytes       
[ 10]   0.00-1.00   sec   128 KBytes  1.05 Mbits/sec    0   39.0 KBytes       
[SUM]   0.00-1.00   sec   640 KBytes  5.24 Mbits/sec    0             
- - - - - - - - - - - - - - - - - - - - - - - - -
[  4]   1.00-2.00   sec  0.00 Bytes  0.00 bits/sec    0   41.4 KBytes       
[  6]   1.00-2.00   sec   128 KBytes  1.05 Mbits/sec    0   45.1 KBytes       
[  8]   1.00-2.00   sec   128 KBytes  1.05 Mbits/sec    0   43.9 KBytes       
[ 10]   1.00-2.00   sec   128 KBytes  1.05 Mbits/sec    0   43.9 KBytes       
[SUM]   1.00-2.00   sec   384 KBytes  3.14 Mbits/sec    0             
- - - - - - - - - - - - - - - - - - - - - - - - -
[  4]   2.00-3.00   sec   128 KBytes  1.05 Mbits/sec    0   46.3 KBytes       
[  6]   2.00-3.00   sec   128 KBytes  1.05 Mbits/sec    0   48.8 KBytes       
[  8]   2.00-3.00   sec   128 KBytes  1.05 Mbits/sec    0   48.8 KBytes       
[ 10]   2.00-3.00   sec   128 KBytes  1.05 Mbits/sec    0   48.8 KBytes       
[SUM]   2.00-3.00   sec   512 KBytes  4.19 Mbits/sec    0             
- - - - - - - - - - - - - - - - - - - - - - - - -
[  4]   3.00-4.00   sec  0.00 Bytes  0.00 bits/sec    0   53.6 KBytes       
[  6]   3.00-4.00   sec   128 KBytes  1.05 Mbits/sec    0   54.8 KBytes       
[  8]   3.00-4.00   sec  0.00 Bytes  0.00 bits/sec    0   54.8 KBytes       
[ 10]   3.00-4.00   sec   128 KBytes  1.05 Mbits/sec    0   54.8 KBytes       
[SUM]   3.00-4.00   sec   256 KBytes  2.10 Mbits/sec    0             
- - - - - - - - - - - - - - - - - - - - - - - - -
[  4]   4.00-5.00   sec   256 KBytes  2.10 Mbits/sec    0   69.5 KBytes       
[  6]   4.00-5.00   sec   128 KBytes  1.05 Mbits/sec    0   73.1 KBytes       
[  8]   4.00-5.00   sec   256 KBytes  2.10 Mbits/sec    0   73.1 KBytes       
[ 10]   4.00-5.00   sec   128 KBytes  1.05 Mbits/sec    0   71.9 KBytes       
[SUM]   4.00-5.00   sec   768 KBytes  6.30 Mbits/sec    0             
^C- - - - - - - - - - - - - - - - - - - - - - - - -
[  4]   5.00-5.84   sec   128 KBytes  1.24 Mbits/sec    0   92.6 KBytes       
[  6]   5.00-5.84   sec   128 KBytes  1.24 Mbits/sec    0   91.4 KBytes       
[  8]   5.00-5.84   sec   128 KBytes  1.24 Mbits/sec    0   93.8 KBytes       
[ 10]   5.00-5.84   sec   128 KBytes  1.24 Mbits/sec    0   97.5 KBytes       
[SUM]   5.00-5.84   sec   512 KBytes  4.96 Mbits/sec    0             
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate         Retr
[  4]   0.00-5.84   sec   768 KBytes  1.08 Mbits/sec    0            sender
[  4]   0.00-5.84   sec  0.00 Bytes  0.00 bits/sec                  receiver
[  6]   0.00-5.84   sec   768 KBytes  1.08 Mbits/sec    0            sender
[  6]   0.00-5.84   sec  0.00 Bytes  0.00 bits/sec                  receiver
[  8]   0.00-5.84   sec   768 KBytes  1.08 Mbits/sec    0            sender
[  8]   0.00-5.84   sec  0.00 Bytes  0.00 bits/sec                  receiver
[ 10]   0.00-5.84   sec   768 KBytes  1.08 Mbits/sec    0            sender
[ 10]   0.00-5.84   sec  0.00 Bytes  0.00 bits/sec                  receiver
[SUM]   0.00-5.84   sec  3.00 MBytes  4.31 Mbits/sec    0             sender
[SUM]   0.00-5.84   sec  0.00 Bytes  0.00 bits/sec                  receiver
iperf3: interrupt - the client has terminated by signal Interrupt(2)
root@OpenWrt:~# iperf3 -c 192.168.14.1 -t 10
iperf3: error - unable to connect to server - server may have stopped running or use a different port, firewall issue, etc.: Connection refused
root@OpenWrt:~# iperf3 -s 
-----------------------------------------------------------
Server listening on 5201 (test #1)
-----------------------------------------------------------
Accepted connection from 192.168.14.1, port 58544
[  5] local 192.168.14.1 port 5201 connected to 192.168.14.1 port 58548
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-1.00   sec  42.4 MBytes   355 Mbits/sec                  
[  5]   1.00-2.00   sec  43.5 MBytes   365 Mbits/sec                  
[  5]   2.00-3.00   sec  43.0 MBytes   361 Mbits/sec                  
[  5]   3.00-4.00   sec  42.0 MBytes   352 Mbits/sec                  
[  5]   4.00-5.00   sec  43.9 MBytes   368 Mbits/sec                  
[  5]   5.00-6.00   sec  42.8 MBytes   359 Mbits/sec                  
[  5]   6.00-7.00   sec  42.2 MBytes   354 Mbits/sec                  
[  5]   7.00-8.01   sec  42.2 MBytes   353 Mbits/sec                  
[  5]   8.01-9.00   sec  41.9 MBytes   353 Mbits/sec                  
[  5]   9.00-10.00  sec  43.9 MBytes   367 Mbits/sec                  
- - - - - - - - - - - - - - - - - - - - - - - - -
[ ID] Interval           Transfer     Bitrate
[  5]   0.00-10.01  sec   428 MBytes   359 Mbits/sec                  receiver
-----------------------------------------------------------
Server listening on 5201 (test #2)
-----------------------------------------------------------

> it was clear that through the LAN connection in the last command line that we used, the result was much faster compared to all of the above

> CGNAT (Carrier-Grade NAT) = ISP-level NAT putting many customers behind one public IPv4 address. DS-Lite = a variant that tunnels IPv4 over an IPv6-only ISP network to a central CGNAT gateway. Home routers are predictable enough for direct P2P; CGNAT/DS-Lite aren't, so they need a relay.
