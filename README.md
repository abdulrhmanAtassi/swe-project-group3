# Smart Home Automation System

## 1. Group Info

| Field | Details |
|---|---|
| **Group Number** | Group 03 |
| **Case Study** | Smart Home Automation System |
| **Course** | Software Engineering |
| **Instructor** | *Dr.Samer Elkababji* |

### Team Members

| Name | Student ID |
|---|---|
| Abdulrhman Atassi | *20210651* |
| Sarah Shobaki | *20220188* |
| Osama Zaid | *20220099* |
| Mariam Laith | *20220872* |

---

## 2. Overview

### System Purpose

The Smart Home Automation System is an IoT-based platform designed to integrate and control smart home devices including thermostats, lighting, security cameras, and alarms. The system enables homeowners and family members to monitor and manage their home environment through mobile and web applications, supporting remote device control, automation routines, and real-time alerts for sensor-triggered events. An embedded AI/ML module learns user behavior patterns to optimize energy efficiency and comfort over time.

### Tools Used

| Tool | Purpose |
|---|---|
| PlantUML | All UML and C4 diagram generation |
| Visual Studio Code | Report and source file editing |
| GitHub | Version control and collaboration |

---

## 3. Diagrams
 
### Part I — Context
 
| ID | Diagram | File | Description |
|---|---|---|---|
| C4-L1 | System Context Diagram | `uml/c4_l1_context.puml` | Shows all actors and external systems interacting with the Smart Home Automation System |
| C4-L2 | Container Diagram | `uml/c4_l2_container.puml` | Breaks the system into deployable containers: clients, API gateway, backend services, IoT gateway, and data layer |
| AD1 | Activity Diagram — Device Control | `uml/ad1_device_control.puml` | Models the end-to-end flow when a user issues a device control command |
| AD2 | Activity Diagram — Automation & AI | `uml/ad2_automation_ai.puml` | Models the background automation trigger and AI suggestion flow |
| AD3 | Activity Diagram — Onboarding | `uml/ad3_onboarding.puml` | Models user registration and device onboarding flow |
| AD4 | Activity Diagram — Alert Response | `uml/ad4_alert_response.puml` | Models the incident detection and emergency response flow |
| AD5 | Activity Diagram — Manage Family | `uml/ad5_manage_family.puml` | Models the homeowner's flow for adding and managing family member accounts |
| AD6 | Activity Diagram — Admin Monitoring | `uml/ad6_admin_monitoring.puml` | Models the system administrator's monitoring and configuration flow |
 
### Part II — Interactions
 
| ID | Diagram | File | Description |
|---|---|---|---|
| UC1 | Use Case Diagram — Users | `uml/uc1_user_interactions.puml` | All use cases available to Homeowner and Family Member |
| UC2 | Use Case Diagram — System & Admin | `uml/uc2_system_admin.puml` | Use cases for System Administrator, Automation Engine, and AI/ML Service |
| SD1 | Sequence Diagram — High Level | `uml/sd1_highlevel.puml` | Stakeholder-level view of the device control flow |
| SD2 | Sequence Diagram — Device Control | `uml/sd2_device_control_detailed.puml` | Detailed developer-level view of device control including cache, DB, and IoT protocol |
| SD3 | Sequence Diagram — Automation & AI | `uml/sd3_automation_detailed.puml` | Detailed flow of sensor-triggered automation and AI pattern recognition |
| SD4 | Sequence Diagram — Onboarding | `uml/sd4_onboarding_detailed.puml` | Detailed flow of user registration and device handshake |
| SD5 | Sequence Diagram — Alert Response | `uml/sd5_alert_detailed.puml` | Detailed flow of anomaly detection, emergency actions, and incident resolution |
| SD6 | Sequence Diagram — Family Member | `uml/sd6_family_member_detailed.puml` | Detailed flow of adding a family member and propagating device permissions |
| SD7 | Sequence Diagram — Admin | `uml/sd7_admin_detailed.puml` | Detailed flow of admin system health monitoring and configuration actions |
 
### Part III — Structure
 
| ID | Diagram | File | Description |
|---|---|---|---|
| CD1 | Class Diagram | `uml/class_diagram.puml` | Full domain model with attributes, operations, generalization, aggregation, and composition |
 
### Part IV — Behavior
 
| ID | Diagram | File | Description |
|---|---|---|---|
| ST1 | State Diagram — Device Lifecycle | `uml/state_diagram_device.puml` | Models all states a device can be in and the events that trigger transitions — event-driven dimension |
| DFD0 | DFD Level 0 — Context | `uml/dfd_l0_context.puml` | System-level data flow context showing external entities and data in/out |
| DFD1 | DFD Level 1 — Data Pipeline | `uml/dfd_l1_pipeline.puml` | Detailed data management pipeline covering user data, device data, AI learning, and reporting |
 
---
 
## 4. Repository Structure
 
```
/
├── README.md                             # This file — also embedded as report title page
├── docs/
│   ├── report.md                         # Full project report in Markdown
│   └── report.pdf                        # Final report converted via Pandoc
└── uml/
    ├── c4_l1_context.puml                # C4 Level 1 — System Context
    ├── c4_l2_container.puml              # C4 Level 2 — Container Diagram
    ├── ad1_device_control.puml           # Activity Diagram 1 — Device Control
    ├── ad2_automation_ai.puml            # Activity Diagram 2 — Automation & AI
    ├── ad3_onboarding.puml               # Activity Diagram 3 — Onboarding
    ├── ad4_alert_response.puml           # Activity Diagram 4 — Alert Response
    ├── ad5_manage_family.puml            # Activity Diagram 5 — Manage Family
    ├── ad6_admin_monitoring.puml         # Activity Diagram 6 — Admin Monitoring
    ├── uc1_user_interactions.puml        # Use Case Diagram 1 — Users
    ├── uc2_system_admin.puml             # Use Case Diagram 2 — System & Admin
    ├── sd1_highlevel.puml                # Sequence Diagram 1 — High Level
    ├── sd2_device_control_detailed.puml  # Sequence Diagram 2 — Device Control
    ├── sd3_automation_detailed.puml      # Sequence Diagram 3 — Automation & AI
    ├── sd4_onboarding_detailed.puml      # Sequence Diagram 4 — Onboarding
    ├── sd5_alert_detailed.puml           # Sequence Diagram 5 — Alert Response
    ├── sd6_family_member_detailed.puml   # Sequence Diagram 6 — Family Member
    ├── sd7_admin_detailed.puml           # Sequence Diagram 7 — Admin
    ├── class_diagram.puml                # Class Diagram — Full Domain Model
    ├── state_diagram_device.puml         # State Diagram — Device Lifecycle
    ├── dfd_l0_context.puml               # DFD Level 0 — Context
    └── dfd_l1_pipeline.puml              # DFD Level 1 — Data Pipeline
```
 
---
 
## 5. Contributions
 
### Member Roles
 
| Member | Role |
|---|---|
| Sarah | System Architect — C4 diagrams, container design |
| Abdulrhman | Interaction Modeler — Use case diagrams and descriptions |
| Mariam | Behavior Modeler — Activity diagrams |
| Osama | Sequence Modeler — Sequence diagrams and report |
 
### Commits Per Member
 
| Member | Commits |
|---|---|
| Sarah | *(32)* |
| Abdulrhman | *(18)* |
| Osama | *(1)* |
| Mariam | *(1)* |


