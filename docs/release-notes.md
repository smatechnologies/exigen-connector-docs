# Release Notes Exigen 21.0

## General

The release removes log4j and replaces it with slj4j and logback.

## Migration Considerations

This release includes the new format installer where the files are extracted from the zip file into the desired directory. 
It contains an embedded java version for the connector so there is no reliance on installed Java versions.

The configuration file has been changed from Agent.config to Connector.config.

### New Features

### Fixes

**CONNUTIL-522**    
                    Update Exigen Connector for CVE-2021-44228 (remove log4j as the logging component and replace with slf4j and logback).
			