# Module 4 — Application Messaging: MQTT Deep Dive & Integration

Date: 27.11.2026  
Pod: 09  
Group: Shuofeng Liu, Max, Julius

<!-- Add links to the group members' portfolios when available. -->

## Learning Goals
**LG1 — MQTT Mechanisms & Protocol Comparison**  
  Explain the MQTT mechanisms — topic hierarchy, QoS levels, retained messages, and the Last Will and Testament — and place MQTT against CoAP and HTTP on the wire: what each costs in transport, latency, and security posture. The layer model itself is Module 1's job, not a second lecture here.  
  **Evidence:** [Task 1 — HTTP Endpoint](#task-1) (HTTP request/response baseline & coupling limits), [Task 2 — MQTT Deep Dive](#task-2) (topic tree, retain, QoS, LWT experiments), and [Study Log](#study-log) (MQTT vs. CoAP vs. HTTP comparison & security posture).

**LG2 — Node-RED Command & Dashboard Flow**  
  Build a command-and-dashboard flow on your pod's Node-RED on the class cluster.  
  **Evidence:** [Task 1 — HTTP Endpoint](#task-1) (Node-RED HTTP endpoint and live temperature dashboard) and [Task 4 — Bridges](#task-4) (multi-protocol Node-RED bridge flows including a reverse command path).

**LG3 — Event-Driven Python Integration**  
  Write an event-driven integration service in Python on your own machine with paho-mqtt, and a small one in MicroPython on the router where the service fits.  
  **Evidence:** [Task 2 — MQTT Deep Dive](#task-2) (Python `paho-mqtt` 2.x publisher & LWT test client in `uv`) and [Task 4 — Bridges](#task-4) (event-driven integration and router command topic handling).

**LG4 — Device Simulation & Decoupled Publisher Swap**  
  Simulate a device before it exists — a fake AC unit with a temperature and an on/off HVAC — and then swap the simulation for another publisher without changing a line downstream.
  **Evidence:** [Task 1 — The Sender](#task-1) (initial simulated Python AC sender), [Task 2 — MQTT Deep Dive](#task-2) (migrating the sender from HTTP to MQTT without rewriting the dashboard logic), and [Task 4 — Bridges](#task-4) (swapping/adding publishers and external triggers with zero downstream changes).

---

## Setup

We use the OpenWrt router setup from Module 2 with Mosquitto running as the pod's lab MQTT broker (`192.168.14.1:1883`, plaintext, restricted to the pod LAN / overlay). Node-RED runs on our pod's instance on the class cluster. Python scripts run on our laptops inside a dedicated `uv` environment (`requests` and `paho-mqtt>=2,<3`).

Group responsibilities: Shuofeng maintains the README, Max collects screenshots and flow exports, and Julius compiles the reflection notes. Each member maintains an individual discussion log and reflection.

---

<a id="task-1"></a>
## HTTP Endpoint & The Sender (Task 1)

**Proves:** LG1, LG2, LG4

### Node-RED HTTP Endpoint
We created an `http in` (`POST /warehouse/temp`) node in our pod's Node-RED flow, parsed the incoming JSON payload, and connected it to a dashboard gauge/display. We verified connectivity from a laptop through the router using `curl`, confirming live updates on the dashboard.

<!-- Add screenshot of the Node-RED HTTP flow and dashboard here. -->

### The Simulated Python Sender
We replaced manual `curl` requests with a Python script (managed via `uv` with `requests`) simulating a cooling unit that sends a drifting temperature reading every two seconds.

### Failure Analysis & Architectural Limits
* **Restarting the sender while Node-RED runs:** The dashboard simply pauses until the sender resumes posting.
* **Stopping/disabling the Node-RED flow while the sender runs:** The Python sender immediately encounters connection errors / HTTP failures because HTTP requires the receiver to be online during the request.
* **What the sender had to know:** The exact host/IP, port, HTTP path (`/warehouse/temp`), and expected JSON schema of the Node-RED endpoint.
* **Adding a second consumer:** Under HTTP, the sender itself (maintained by the device/sensor developer) would have to be modified to send a second request to the new consumer's address—creating tight point-to-point coupling.

---

<a id="task-2"></a>
## Topic Plan & MQTT Experiments (Task 2)

**Proves:** LG1, LG3, LG4

### Topic Plan
Since our pod owns its own Mosquitto broker, we designed a clean, flat hierarchy for the simulated cooling unit:

```text
cold/
  ac/
    env      # Sensor readings (temperature / environment JSON)
    set      # Incoming HVAC commands (e.g., ON / OFF)
    status   # Device availability ("online" / "offline" via LWT)
