# System Architecture

## Pipeline Overview

Client CSV → TecOps Agent → HANDOFF → ROI Agent → Report

## Agent 1: TecOps Diagnostics

**Input:** Route/orders CSV + telematics CSV + client context  
**Model:** Gemini 2.5 Pro via Gemini API  
**Processing:** 4 diagnostic layers  
**Output:** Structured findings + HANDOFF block

### Diagnostic Layers
1. Validation — missing fields, out-of-range config values
2. Technical — sensor failures, false alarms, calibration drift
3. Operational — cold chain breaches, unregistered door openings
4. Route/Time — systematic overtime, unmapped shortcuts

## Agent 2: ROI Calculator

**Input:** HANDOFF block from TecOps Agent  
**Model:** Gemini 2.5 Pro via Gemini API  
**Processing:** Per-vehicle economic quantification  
**Output:** USD impact per vehicle + confidence levels

### Key Rules
- Frequency calculated from CSV data — never estimated freely
- Per-vehicle calculation — never aggregated across vehicles
- Statistical confidence: BAJA (<7 days) / MEDIA (7-30) / ESTÁNDAR (>30)
- Verified data separated from assumptions in every output

## Client Intake Flow

1. Client submits CSV via Google Forms
2. Files stored in Google Drive
3. TecOps Agent processes via Gemini API
4. HANDOFF passed to ROI Calculator
5. Operator validates output
6. Report delivered in 48 hours

## Test Dataset

Synthetic 18-truck fleet (dairy and poultry, Buenos Aires)  
3-day period, 15 route orders, 36 telemetry records  
6 planted anomalies — detection rate: 6/6, false positives: 0
