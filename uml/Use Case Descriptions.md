### 3.2 Use Case Descriptions

Detailed tabular descriptions are provided for the eight primary use cases — one per major functional area. Each table includes preconditions, postconditions, main flow, alternate flows, exceptions, and UML relationships.

Use cases following standard read-only or simple CRUD patterns (View Device Status, View System Dashboard, Monitor System Health, Manage Device Configurations) are self-documented by the use case diagrams and do not introduce new architectural interactions beyond those modeled in the sequence diagrams.

---

#### UC-01: Log In

| Field | Description |
|---|---|
| **Use Case ID** | UC-01 |
| **Use Case Name** | Log In |
| **Actor(s)** | Homeowner, Family Member |
| **Description** | A registered user authenticates into the system using their credentials to gain access to permitted features |
| **Preconditions** | User has a registered and verified account |
| **Postconditions** | User is authenticated and redirected to the system dashboard |
| **Main Flow** | 1. User opens mobile or web app. 2. User enters email and password. 3. App sends credentials to API Gateway. 4. API Gateway forwards to Authentication Service. 5. Authentication Service validates credentials and returns JWT token. 6. System grants access based on user role |
| **Alternate Flow** | 3a. Invalid credentials → system displays error and prompts retry. 3b. Account not verified → system prompts email verification |
| **Exceptions** | Account locked after 5 failed attempts. Network failure → system displays connection error |
| **Includes** | — |
| **Extends** | — |

---

#### UC-02: Control Device

| Field | Description |
|---|---|
| **Use Case ID** | UC-02 |
| **Use Case Name** | Control Device |
| **Actor(s)** | Homeowner, Family Member |
| **Description** | An authenticated user sends a control command to a smart device such as turning lights on/off or adjusting thermostat temperature |
| **Preconditions** | User is logged in. Target device is registered and online. User has permission to control the target device |
| **Postconditions** | Device executes the command. State is updated in cache and database. User receives confirmation |
| **Main Flow** | 1. User selects target device from app. 2. User issues control command. 3. App sends request to API Gateway. 4. Gateway validates authentication and permission. 5. Device Management Service forwards command to IoT Gateway. 6. IoT Gateway translates and dispatches to physical device. 7. Device acknowledges command. 8. State updated in cache and database. 9. Confirmation sent to user |
| **Alternate Flow** | 7a. Device does not acknowledge → IoT Gateway retries up to 3 times. 7b. All retries fail → system reports device failure and triggers alert |
| **Exceptions** | Device offline → system displays offline message. Permission denied → system returns 403 error |
| **Includes** | UC-01 Log In |
| **Extends** | UC-06 Trigger Alert |

---

#### UC-03: Add / Remove Device

| Field | Description |
|---|---|
| **Use Case ID** | UC-03 |
| **Use Case Name** | Add / Remove Device |
| **Actor(s)** | Homeowner |
| **Description** | The homeowner registers a new smart device to the household or removes an existing one from the system |
| **Preconditions** | User is logged in as Homeowner. For adding: device is physically powered and within communication range |
| **Postconditions** | Device is registered/removed in the central database. IoT Gateway establishes or terminates communication channel |
| **Main Flow** | 1. Homeowner navigates to device management. 2. Selects Add Device. 3. Scans QR code or enters device ID. 4. Device Management Service validates ID. 5. System registers device to household. 6. IoT Gateway performs handshake with physical device. 7. Device status set to Online. 8. Homeowner assigns name, room, and preferences |
| **Alternate Flow** | 4a. Device ID already registered → system returns conflict error. 6a. Handshake fails → device set to Unreachable, user notified |
| **Exceptions** | Invalid device ID → system rejects registration. Network failure during handshake → system prompts retry |
| **Includes** | UC-01 Log In |
| **Extends** | — |

---

#### UC-04: Create Automation Rule

| Field | Description |
|---|---|
| **Use Case ID** | UC-04 |
| **Use Case Name** | Create Automation Rule |
| **Actor(s)** | Homeowner |
| **Description** | The homeowner defines a trigger-based automation rule that instructs the system to perform device actions automatically when specified conditions are met |
| **Preconditions** | User is logged in as Homeowner. At least one device is registered |
| **Postconditions** | Automation rule is saved to database. Automation Engine begins evaluating rule against incoming events |
| **Main Flow** | 1. Homeowner navigates to automation settings. 2. Selects Create New Rule. 3. Defines trigger condition (e.g. motion detected, time schedule). 4. Defines action (e.g. turn on lights, send alert). 5. Saves rule. 6. System stores rule in database. 7. Automation Engine registers rule for evaluation |
| **Alternate Flow** | 5a. Rule conflicts with existing rule → system warns user and requests confirmation |
| **Exceptions** | Invalid trigger or action configuration → system displays validation error |
| **Includes** | UC-01 Log In |
| **Extends** | UC-08 Generate Automation Suggestion |

---

#### UC-05: Manage Family Members

| Field | Description |
|---|---|
| **Use Case ID** | UC-05 |
| **Use Case Name** | Manage Family Members |
| **Actor(s)** | Homeowner |
| **Description** | The homeowner adds, removes, or modifies household member accounts and assigns device access permissions to each member |
| **Preconditions** | User is logged in as Homeowner |
| **Postconditions** | Family member account is created, updated, or removed. Permissions are propagated to the Device Management Service and reflected in device access control lists |
| **Main Flow** | 1. Homeowner navigates to household management. 2. Selects Add Member. 3. Enters member name and email. 4. Assigns role and device permissions. 5. System creates pending account and sends invitation email. 6. Member accepts invitation and sets password. 7. Account activated with assigned permissions. 8. Permissions propagated to Device Management Service |
| **Alternate Flow** | 3a. Email already registered → system links existing account to household. 6a. Invitation not accepted within 48 hours → invitation expires |
| **Exceptions** | Maximum household member limit reached → system rejects addition |
| **Includes** | UC-01 Log In |
| **Extends** | — |

---

#### UC-06: Trigger Alert

| Field | Description |
|---|---|
| **Use Case ID** | UC-06 |
| **Use Case Name** | Trigger Alert |
| **Actor(s)** | Automation Engine |
| **Description** | The Automation Engine detects an anomalous device event or failed command and dispatches a high-priority alert to the homeowner via the Notification Service |
| **Preconditions** | A sensor event or device failure has occurred. Notification Service is operational |
| **Postconditions** | Alert is delivered to homeowner via push notification and/or email. Incident is logged to database |
| **Main Flow** | 1. Automation Engine detects anomalous event. 2. Classifies alert severity (Low/Medium/High). 3. Forwards to Notification Service. 4. Notification Service dispatches push and email alert. 5. Homeowner receives and acknowledges alert. 6. Incident logged to database |
| **Alternate Flow** | 4a. Push notification fails → system falls back to email only |
| **Exceptions** | Notification Service unavailable → incident logged locally and alert queued for retry |
| **Includes** | — |
| **Extends** | UC-02 Control Device |

---

#### UC-07: Execute Automation Rule

| Field | Description |
|---|---|
| **Use Case ID** | UC-07 |
| **Use Case Name** | Execute Automation Rule |
| **Actor(s)** | Automation Engine |
| **Description** | The Automation Engine evaluates active rules against incoming device state changes and executes matched actions automatically without human input |
| **Preconditions** | At least one automation rule exists in the database. A device state change event has been received from the Device Management Service |
| **Postconditions** | Matched actions are executed. Execution is logged. User is notified if rule specifies notification |
| **Main Flow** | 1. Device state change received from Device Management Service. 2. Automation Engine loads active rules from database. 3. Evaluates each rule against current state. 4. Identifies matching rules. 5. Dispatches action commands to Device Management Service. 6. Logs execution to database. 7. Sends confirmation notification if configured |
| **Alternate Flow** | 4a. No rule matches → engine logs event and takes no action |
| **Exceptions** | Rule references a deleted device → engine skips rule and flags it for review |
| **Includes** | — |
| **Extends** | — |

---

#### UC-08: Generate Automation Suggestion

| Field | Description |
|---|---|
| **Use Case ID** | UC-08 |
| **Use Case Name** | Generate Automation Suggestion |
| **Actor(s)** | AI / ML Service |
| **Description** | The AI/ML Service analyzes historical user behavior and device usage patterns to generate personalized automation rule suggestions for the homeowner |
| **Preconditions** | Sufficient usage history exists in the database (minimum data threshold met). AI/ML Service is operational |
| **Postconditions** | Suggestion is either auto-applied if enabled, or sent to homeowner for review via Notification Service |
| **Main Flow** | 1. AI/ML Service reads usage history from database. 2. Identifies recurring behavior patterns. 3. Generates automation suggestion. 4. Checks if homeowner has auto-apply enabled. 5a. If yes → submits rule to Automation Engine directly. 5b. If no → sends suggestion to Notification Service for user review. 6. Homeowner accepts or rejects suggestion |
| **Alternate Flow** | 3a. No significant pattern detected → service logs attempt and schedules next analysis |
| **Exceptions** | Insufficient data → suggestion generation skipped until minimum data threshold is met |
| **Includes** | — |
| **Extends** | UC-04 Create Automation Rule |
