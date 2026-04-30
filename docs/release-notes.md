---
sidebar_label: 'Release notes'
title: Exigen Connector release notes
description: "Version history and change details for the Exigen Connector, including new features, improvements, and bug fixes."
tags:
  - Reference
  - System Administrator
  - Automation Engineer
  - Getting Started
---

# Exigen Connector release notes

## 21

### 21.0.0

**Released:** 2022

### What's new

:eight_spoked_asterisk: **CONNUTIL-522**: Removed log4j as the logging component and replaced it with slf4j and logback to address CVE-2021-44228.

### Why this matters

Removing log4j eliminates exposure to CVE-2021-44228, a critical remote code execution vulnerability. The connector now uses slf4j and logback for logging, which are not affected by this vulnerability.

### Migration notes

- This release uses a new installer format. Extract the files from the zip file into the desired directory.
- The connector includes an embedded Java environment, eliminating any dependency on Java versions installed on the host system.
- The configuration file has been renamed from `Agent.config` to `Connector.config`. Update any references to the configuration file path after upgrading.
