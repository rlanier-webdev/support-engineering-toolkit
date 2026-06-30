# Intake & Triage Framework

A structured system for converting incoming support tickets into clear, actionable technical work.

This framework is used to reduce ambiguity, speed up triage, and ensure consistent handling of customer issues across severity levels and complexity.


## Purpose

Support tickets often arrive incomplete, unclear, or misaligned with the actual underlying technical issue.

This framework ensures every ticket is:

- Normalized into a consistent structure
- Evaluated for completeness before investigation
- Classified by impact and urgency
- Either made actionable or sent back for clarification


## How This Folder Works

This folder represents the first stage of the support engineering workflow.

Everything here happens BEFORE debugging, API analysis, or escalation.

If a ticket cannot pass this stage, it should NOT move forward.


## Components

### 01. Intake Template
Standard structure for capturing:
- user intent
- problem statement
- impact
- environment context
- evidence
- reproduction steps

### 02. Severity Classification
Defines impact levels (SEV1–SEV4) to determine urgency and response path.

### 03. Actionability Check
A strict gate to determine whether enough information exists to begin investigation.

### 04. Missing Information Prompts
Reusable communication templates for quickly requesting missing context from customers.


## Workflow Summary

1. Ticket is received  
2. Intake template is filled  
3. Severity is assigned  
4. Actionability is evaluated  
5. If incomplete → request missing info  
6. If actionable → proceed to technical investigation  


## Key Principle

Do not start debugging incomplete problems.

Clarify first. Investigate second.


## Outcome

Using this framework reduces:
- wasted investigation time
- back-and-forth with customers
- inconsistent severity classification
- premature escalation

And improves:
- triage speed
- signal quality
- engineering handoff readiness