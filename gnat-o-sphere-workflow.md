# GNAT-o-Sphere Canonical Workflow

**Date:** 2026-04-22

This document provides a single end-to-end operator workflow for the GNAT-o-sphere ecosystem.

## Purpose

The ecosystem is strongest when described as a connected operational flow instead of a set of adjacent projects. This document explains the intended path from telemetry and indicators to correlation, validation, and reporting.

## Core Components

- **GNAT** — investigation hub, connector platform, STIX-centric correlation and reporting
- **SenseGNAT** — behavioral profiling and anomaly detection on network telemetry
- **SandGNAT** — malware detonation and artifact enrichment
- **RedGNAT** — adversary emulation and validation

## Architectural View

The workflow spans two connected planes:

### 1. Telemetry Plane

Raw flow and operational telemetry enters the ecosystem. SenseGNAT consumes GNAT's Kafka telemetry stream before GNAT converts records to STIX.

This is where behavioral logic benefits from fields such as:

- source and destination IP
- destination port
- protocol
- byte counts
- session-level context

### 2. Intelligence Plane

Normalized findings are correlated and represented in structured investigation workflows. GNAT acts as the primary hub for evidence, relationships, reporting, and downstream publication.

## Canonical End-to-End Flow

### Step 1: Telemetry and Source Collection

GNAT ingests and routes telemetry, connector outputs, and source intelligence into the ecosystem.

### Step 2: Behavioral Profiling with SenseGNAT

SenseGNAT consumes telemetry directly from the Kafka stream (`gnat.telemetry` by default) and applies behavioral profiling and anomaly detection before STIX transformation removes useful flow-level detail.

Outputs may include:

- anomaly findings
- narratives
- confidence or explanation metadata
- normalized detection outputs for GNAT consumption

### Step 3: Malware Detonation with SandGNAT

Suspicious files, URLs, or derived artifacts are detonated and analyzed in SandGNAT.

Outputs may include:

- static and dynamic observations
- extracted indicators
- CAPA/YARA-derived findings
- sandbox artifacts and bundles

### Step 4: Detection Validation with RedGNAT

Where defensive confidence or coverage validation is required, RedGNAT performs controlled adversary emulation and returns findings about:

- detection coverage
- response gaps
- validation results
- structured notes for investigation follow-up

### Step 5: Correlation in GNAT

GNAT consumes and correlates outputs from connectors and addons into an investigation context that can include:

- indicators
- observations
- behavioral findings
- detonation findings
- emulation findings
- linked evidence and campaign context

### Step 6: Reporting and Operator Action

The investigator or analyst uses GNAT to:

- pivot across evidence
- build case context
- assess confidence
- publish reports
- export structured findings

## Why This Workflow Matters

This workflow expresses the actual intended platform value:

- GNAT is the hub
- SenseGNAT adds telemetry-native behavioral context
- SandGNAT adds malware and artifact analysis depth
- RedGNAT adds controlled validation and coverage testing

Together, they support a full path from **signal** to **investigation** to **validation** to **reporting**.

## Recommended Follow-On Documentation

To reinforce this model, add or update:

- GNAT README ecosystem section
- GNAT docs explanation pages
- top-level GNAT-o-sphere landing content
- diagrams used in presentations and architecture reviews
