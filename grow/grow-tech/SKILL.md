---
name: grow-tech
description: Dual-environment execution loop to monitor, cross-reference, and optimize independent grow operations.
version: 1.2.0
---

# Skill: Dual-Context Grow Health Report

## Core Operational Directives

### 1. Unified Nomenclature Compliance
- You are optimizing two distinct spaces: **Grow Room 1** and **Grow Room 2**. Do not refer to them as Tent Alpha or Bravo. 
- Evaluate Grow Room 1 entirely, then evaluate Grow Room 2 entirely. Never average, blend, or bleed parameters between these distinct microclimates.
- For **Grow Room 1** details, load the reference: `skill_view("grow-tech", "references/GROWROOM1.md")`
- For **Grow Room 2** details, load the reference: `skill_view("grow-tech", "references/GROWROOM2.md")`
- For every report, load the reference: `skill_view("grow-tech", "references/LUNGROOM.md")`

### 2. Data Acquisition Protocol
- **Grow Log:** Retrieve the grow log notes for the last 7 days for each room using `ha_get_history(entity_ids=["sensor.<sensor_name>"], start_time="7d")`
- **Real-time Sensors:** Get the current state for the sensors marked **Real-time Sensors** using home_assistant `ha_get_state(["sensor.<sensor_name>"], fields=["state"])`. Use a list to retrieve all real-time sensor states in a single API call for each grow room.
- **Historical Sensors:** Get the last 24 hours history summarized from statistics for the sensors marked **Historical Sensors** using home_assistant
```
ha_get_history(source="statistics", entity_ids=["sensor.<sensor_name>"], start_time="24h", period="day", statistic_types=["mean", "min", "max"])
```

### 3. Advanced Botanical Insights
- **Direct Leaf VPD Utilization:** The provided VPD sensor metrics represent the actual *Leaf VPD* (accounting for canopy dynamics). Use these numbers directly to map against target thresholds for the specific `Grow Phase` (e.g., 0.8–1.2 kPa for vegetative growth, 1.2–1.6 kPa for flower).
- **Trend Diagnostics:** Analyze the 24-hour history for each historical sensor. Ensure the mean, min and max values are within healthly range.
- **Soil Moisture:** Analyze the soil moisture percentages. Cross-reference these percentages with the current grow phase to evaluate dry-back progression. Determine if the current moisture percentage is optimal for root zone oxygenation, or if it indicates saturation or depletion thresholds that require triggering the irrigation valves.
- **Equipment Usage:** Analyze the exhaust fan usage patterns. Correlate excessive runtime with potential heat or humidity issues. Correlate insufficient runtime with potential air circulation or odor control issues.

### 4. Grow Room Details
- Soil Moisture Sensor Position: 4.5" Depth
- Grow Room 1: 4x4 ft, 3 plants in 7-gallon fabric pots
- Grow Room 2: 5x5 ft, 4 plants in 7-gallon fabric pots

## Required Report Output Schema
For every execution cycle, format your output exactly as follows:

### 🟢 Grow Room x Analysis
- **Current Lifecycle:** [Days since Start Date] | [Phase]
- **Leaf VPD & Transpiration Health:** [Sensor Leaf VPD vs Target Range]
- **Trend Line Review:** [Analysis of 24-hour mean, min, max values for historical sensors]
- **Action Items:** [Specific hardware or programmatic adjustments]

### 🌐 Macro-Infrastructure Correlation
- **Lung Room Status:** [Evaluation of shared room ambient performance]
- **Equipment Usage:** [Correlation of equipment usage patterns with environmental conditions]
- **Diagnosis:** [Cross-room data synthesis identifying root-cause infrastructure faults]