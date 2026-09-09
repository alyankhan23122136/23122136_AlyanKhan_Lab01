# 23122136 Alyan Ali Ahmed Khan

# Intelligent Agents Assignment

## Maintain AI — Intelligent Facility Maintenance \& Repair Prioritization Agent

**Student Name:** Alyan Ali Ahmed Khan  
**Roll Number:** 23122136  
**Section:** A 
**Semester:** 6

\---

## Project Overview

This repository contains my **Intelligent Agents assignment** and a Python-based implementation of **Maintain AI**, an intelligent facility maintenance, fault-identification, repair, and prioritization agent.

The purpose of this agent is to analyze maintenance complaints, equipment condition, operational impact, technician availability, and spare-part status in order to decide:

* Which maintenance problem should be handled first
* What the likely causes of the fault may be
* What repair or maintenance action should be taken
* Whether the issue should be escalated
* Which technician or maintenance team is required
* Whether preventive maintenance should be scheduled

The goal of **Maintain AI** is to reduce safety risk, minimize equipment downtime, improve maintenance response, and use available maintenance resources efficiently.

\---

## Problem Statement

Facility maintenance teams often receive multiple faults at the same time.

If maintenance requests are handled only according to reporting time, a minor problem may be repaired before a safety-critical fault.

For example:

* An elevator reports abnormal vibration
* A classroom air conditioner stops cooling
* A corridor light stops working

The system should not simply follow the order in which these problems were reported. The elevator fault may require immediate attention because of its higher safety and operational risk.

Maintain AI solves this problem by analyzing the fault, estimating its priority, and recommending an appropriate maintenance action.

\---

## Main Features

Maintain AI can:

* Identify facility maintenance problems
* Analyze possible causes of faults
* Evaluate safety risk
* Evaluate operational impact
* Prioritize multiple maintenance requests
* Recommend repair or maintenance actions
* Suggest the required technician specialization
* Identify possible spare-part requirements
* Escalate critical faults
* Recommend preventive maintenance
* Identify missing information needed for better diagnosis

\---

## How the Agent Works

The agent follows a perception-action cycle:

```text
Receive Complaint / Sensor Data
            ↓
Identify Asset and Location
            ↓
Analyze Symptoms
            ↓
Assess Safety Risk
            ↓
Assess Operational Impact
            ↓
Determine Priority
            ↓
Check Technician / Spare-Part Requirements
            ↓
Recommend Repair, Schedule, Monitor, or Escalate
            ↓
Collect Feedback and Update Maintenance History
```

\---

## Percepts / Inputs

The agent can use the following information:

### Maintenance Complaint

* Issue type
* Location
* Reported severity
* Time of report

### Equipment Condition

* Temperature
* Vibration
* Runtime
* Alarms
* Abnormal noise
* Leakage
* Electrical symptoms
* Sensor readings

### Asset Information

* Equipment age
* Criticality
* Previous breakdowns
* Repair history
* Service interval

### Operational Impact

* Number of people affected
* Building zone
* Occupancy
* Operating hours

### Resource Status

* Technician skills
* Technician availability
* Spare-part availability
* Estimated repair time

\---

## Priority Levels

|Priority|Description|
|-|-|
|**CRITICAL**|Immediate safety danger, major failure, serious electrical/fire/gas/elevator/structural risk|
|**HIGH**|Important failure with major operational impact or potential safety concern|
|**MEDIUM**|Moderate disruption with no immediate serious safety threat|
|**LOW**|Minor fault with limited impact that can safely be scheduled|

Safety always receives the highest priority.

\---

## PEAS Analysis

|Component|Details|
|-|-|
|**P — Performance Measure**|Minimize safety risk and downtime, improve response to critical faults, improve uptime, support preventive maintenance, and use technicians and spare parts efficiently|
|**E — Environment**|Campus/building facilities, HVAC, elevators, electrical and plumbing systems, maintenance staff, spare-parts inventory, occupied areas, and operating schedules|
|**A — Actuators**|Re-prioritize work orders, assign technicians, schedule repairs, schedule preventive maintenance, escalate critical incidents, issue alerts, and update work-order status|
|**S — Sensors**|Maintenance tickets, IoT/BMS readings, equipment alarms, asset history, repair history, occupancy data, technician availability, spare-part status, and repair feedback|

\---

## Environment Properties

|Property|Type|Reason|
|-|-|-|
|**Observability**|Partially Observable|Complaints, sensors, and records may not reveal every hidden defect|
|**Determinism**|Stochastic / Uncertain|Faults can worsen, resources can change, and new readings can affect priority|
|**Episodes**|Sequential|Current maintenance decisions affect future risk and resource availability|
|**Change**|Dynamic|Faults, occupancy, equipment condition, and technician availability can change|
|**Values**|Mixed|Priority states are discrete while sensor values such as temperature and vibration are continuous|
|**Agents**|Single Agent|Maintain AI is the main autonomous reasoning agent|

\---

## Repository Contents

|File|Description|
|-|-|
|`Intelligent\_Agent\_Assignment.pdf`|Complete Intelligent Agents assignment report|
|`Alyan\_23122136.ipynb`|Google Colab notebook containing the Maintain AI implementation|
|`README.md`|Project documentation and instructions|



\---

## Maintain AI Example

### Example Input

```text
Elevator in Block A is producing abnormal vibration.
The AC in Classroom 5 is not cooling.
One corridor light in Block C is not working.
```

### Expected Agent Behavior

```text
1. Elevator abnormal vibration — HIGH / CRITICAL
   Reason: Possible safety and service risk.

2. Classroom AC not cooling — MEDIUM
   Reason: Operational impact but usually no immediate safety danger.

3. Corridor light failure — LOW
   Reason: Minor fault unless the area becomes unsafe because of poor lighting.
```

The final priority depends on the information available to the agent.

\---

## Python Implementation

```python
!pip install -q -U google-genai

from google import genai
from google.colab import userdata

api\_key = userdata.get("GEMINI\_API\_KEY")
client = genai.Client(api\_key=api\_key)

MODEL = "gemini-2.5-flash"


def maintain\_ai(user\_input):

    prompt = f"""
You are Maintain AI, an intelligent facility maintenance,
fault identification, repair, and prioritization agent.

Your tasks are to:

1. Identify the maintenance problem
2. Identify possible causes
3. Assess safety risk
4. Assess operational impact
5. Assign a priority level
6. Recommend a solution
7. Recommend repair or maintenance action
8. Suggest the required technician
9. Identify possible spare-part needs
10. Decide whether escalation is required
11. Recommend preventive maintenance
12. State any missing information

Priority Levels:
CRITICAL, HIGH, MEDIUM, LOW

Important Rules:
- Safety always has the highest priority.
- Do not invent missing information.
- If several faults are given, rank all faults.
- Explain why one fault has a higher priority than another.
- For dangerous systems, recommend qualified personnel instead of unsafe DIY repair.

Facility Report:
{user\_input}

Maintain AI Decision:
"""

    response = client.models.generate\_content(
        model=MODEL,
        contents=prompt
    )

    return response.text


print("Maintain AI Started (type 'exit' to stop)\\n")

while True:
    user = input("Facility Report: ").strip()

    if user.lower() in \["exit", "quit", "bye"]:
        print("Maintain AI stopped.")
        break

    try:
        reply = maintain\_ai(user)
        print("\\nMaintain AI Report:\\n")
        print(reply)

    except Exception as e:
        print("Error:", e)
```

\---

## How to Run

1. Open the notebook in **Google Colab**.
2. Install the Gemini Python SDK:

```python
!pip install -U google-genai
```

3. Open **Colab → Secrets**.
4. Add a secret named:

```text
GEMINI\_API\_KEY
```

5. Paste your Gemini API key as its value.
6. Enable **Notebook Access**.
7. Run the notebook cells.
8. Enter a facility maintenance problem.

Example:

```text
Facility Report: AC in classroom 5 is not cooling
```

\---

## Technologies Used

* Python
* Google Colab
* Google Gemini API
* `google-genai`
* Prompt Engineering
* Intelligent Agent Concepts
* PEAS Model
* Facility Maintenance Decision Support

\---

## Agent Decision Model

```text
Perceive
   ↓
Identify Problem
   ↓
Analyze Possible Causes
   ↓
Assess Risk
   ↓
Prioritize
   ↓
Recommend Solution
   ↓
Assign / Schedule / Escalate / Monitor
   ↓
Prevent Future Failure
```

\---

## Important Note

Maintain AI is designed as an **educational intelligent-agent project**.

Its repair suggestions should be treated as decision support. Safety-critical systems such as elevators, high-voltage electrical equipment, gas systems, fire-protection systems, and structural faults should be inspected and repaired by qualified professionals.

\---

## Author

**Alyan Ali Ahmed Khan**  
**Roll Number:** 23122136  
**Intelligent Agents Assignment**

