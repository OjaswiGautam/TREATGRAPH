# TREATGRAPH

**Graph-Based AI for Enterprise Cyber Threat Detection & SOC Investigation**

TREATGRAPH is an AI-driven cybersecurity framework that models enterprise telemetry—users, devices, processes, DNS, and network flows—as a **continuously updated temporal heterogeneous graph**. Instead of treating alerts in isolation, TREATGRAPH correlates weak, distributed signals across time to surface multi-stage attack paths (such as lateral movement, privilege escalation, command-and-control, and data exfiltration) and translates them into MITRE ATT&CK-aligned explanations for SOC analysts.

> **Scope Note:** TREATGRAPH is designed as a **SOC Investigation & Correlation Assistant** to reduce alert fatigue and prioritize coordinated threats—not an autonomous, black-box blocking system.

---

## Why Graphs?

Traditional security tools operate in silos:
* **SIEMs** rely on static rules that struggle to catch novel, multi-stage attacks.
* **EDR, NDR, and UEBA** monitor endpoints, network flows, and user logins separately, missing the cross-domain chain connecting them.

Enterprise attacks are inherently **relational and temporal**. A compromised account logging into a workstation, spawning an unusual process, resolving a rare domain, and transferring data outward may look benign as four separate events—but as a connected path over time, it tells a clear story.

---

## Core Capabilities

* **Unified Temporal Heterogeneous Graph:** Models typed entities (`User`, `Host`, `Process`, `IP/Domain`, `Privilege`) and time-stamped interactions (`authenticated-as`, `executed`, `connected-to`, `resolved-DNS`) using rolling time windows and edge decay.
* **Low-Label Anomaly Detection:** Combines unsupervised anomaly scoring (to flag rare structural and behavioral patterns) with semi-supervised ranking (leveraging scarce red-team events and analyst feedback).
* **Multi-Hop Attack-Path Scoring:** Evaluates full entity chains rather than isolated alerts, prioritizing paths that touch high-privilege accounts or critical assets.
* **Explainable SOC Triage:** Maps suspicious subgraphs to **MITRE ATT&CK** tactics (*Lateral Movement, Privilege Escalation, Command & Control, Exfiltration*), providing human-readable evidence chains and an analyst feedback loop.

---

## System Architecture

```text
[ Enterprise Telemetry: Auth, Process, DNS, Flows, Alerts ]
                            │
                            ▼
  1. Ingestion & Entity Resolution  (Normalize users, hosts, IPs, processes)
                            │
                            ▼
  2. Temporal Graph & Feature Layer (Rolling snapshots, peer-group baselines)
                            │
                            ▼
  3. Graph Learning Layer           (Heterogeneous / Temporal GNN embeddings)
                            │
                            ▼
  4. Anomaly & Risk Scoring         (Unsupervised scoring + semi-supervised ranking)
                            │
                            ▼
  5. Path Correlation & Explanation (Subgraph extraction + MITRE ATT&CK mapping)
                            │
                            ▼
  6. SOC Investigation Workbench    (Interactive graph, timeline, analyst feedback)