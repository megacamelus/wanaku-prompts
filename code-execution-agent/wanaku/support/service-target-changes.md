# ServiceTarget Refactoring - Breaking Changes

## Overview

This document describes the breaking changes made to the `ServiceTarget` class and the service discovery API registration process as part of the code execution engine implementation.

## Changes Made

### 1. Field Renaming

**Before:**
```java
private String service;
```

**After:**
```java
private String serviceName;
```

**Impact:** All code using `getService()` must be updated to use `getServiceName()`.

### 2. ServiceType Enum Replacement

**Before:**
```java
private ServiceType serviceType; // enum with RESOURCE_PROVIDER, TOOL_INVOKER, MULTI_CAPABILITY
```

**After:**
```java
private String serviceType;
private String serviceSubType;
```

**Impact:**
- ServiceType is now a string instead of an enum
- New optional `serviceSubType` field added for finer-grained service classification
- String values: "resource-provider", "tool-invoker", "multi-capability", "code-execution-engine"

### 3. Constructor Changes

**Before:**
```java
public ServiceTarget(String id, String service, String host, int port, ServiceType serviceType)
```

**After:**
```java
public ServiceTarget(String id, String serviceName, String host, int port, String serviceType, String serviceSubType)
```

### 4. Factory Method Changes

**Before:**
```java
ServiceTarget.newEmptyTarget(String service, String address, int port, ServiceType serviceType)
```

**After:**
```java
// With subtype
ServiceTarget.newEmptyTarget(String serviceName, String address, int port, String serviceType, String serviceSubType)

// Without subtype (backward compatibility helper)
ServiceTarget.newEmptyTarget(String serviceName, String address, int port, String serviceType)
```

### 5. New Getter/Setter Methods

Added:
- `getServiceName()` / `setServiceName(String)`
- `setServiceType(String)`
- `getServiceSubType()` / `setServiceSubType(String)`

Removed:
- `getService()` (replaced by `getServiceName()`)

## Files Modified

### Core API
- `capabilities-api/src/main/java/ai/wanaku/capabilities/sdk/api/types/providers/ServiceTarget.java`

### Data Files Module
- `capabilities-data-files/src/main/java/ai/wanaku/capabilities/sdk/data/files/InstanceDataManager.java`
    - Updated `newFileHeader()` to use string-based service types
    - Added support for "code-execution-engine" service type
- `capabilities-data-files/src/test/java/ai/wanaku/capabilities/sdk/data/files/InstanceDataManagerTest.java`

### Discovery Module
- `capabilities-discovery/src/main/java/ai/wanaku/capabilities/sdk/discovery/DiscoveryLogCallback.java`
- `capabilities-discovery/src/main/java/ai/wanaku/capabilities/sdk/discovery/ZeroDepRegistrationManager.java`

### Archetypes
- `capabilities-archetypes/capabilities-archetypes-java-tool/src/main/resources/archetype-resources/src/main/java/App.java`

## Migration Guide

### For Existing Code

**Old Code:**
```java
ServiceTarget target = ServiceTarget.newEmptyTarget(
    "my-service", 
    "localhost", 
    9190, 
    ServiceType.TOOL_INVOKER
);
String serviceName = target.getService();
String type = target.getServiceType().asValue();
```

**New Code:**
```java
ServiceTarget target = ServiceTarget.newEmptyTarget(
    "my-service", 
    "localhost", 
    9190, 
    "tool-invoker"
);
String serviceName = target.getServiceName();
String type = target.getServiceType();
```

### For Code Execution Engine

**New Usage:**
```java
ServiceTarget target = ServiceTarget.newEmptyTarget(
    "java-executor",
    "localhost",
    9190,
    "code-execution-engine",
    "jvm"
);
```

## Service Type Values

### Standard Service Types
- `"resource-provider"` - Provides resources
- `"tool-invoker"` - Invokes tools
- `"multi-capability"` - Can do both
- `"code-execution-engine"` - Executes code

### Service SubTypes (for code-execution-engine)
- `"jvm"` - Java Virtual Machine based engines
- `"interpreted"` - Interpreted scripting languages
- `null` - No subtype (for other service types)

## Backward Compatibility

### Breaking Changes
This is a **major version change** with breaking API changes:
1. Method `getService()` removed - use `getServiceName()`
2. `ServiceType` enum replaced with `String` - use string literals
3. Constructor signature changed - added `serviceSubType` parameter

### Compatibility Helpers
- Overloaded `newEmptyTarget()` method without `serviceSubType` parameter
- `InstanceDataManager` maps "code-execution-engine" to MULTI_CAPABILITY for file headers

## Validation

All changes have been validated:
- ✅ Full project compilation successful
- ✅ All modules compile without errors
- ✅ ServiceTarget refactoring complete
- ✅ Discovery API updated
- ✅ Data files module updated
- ✅ Archetype templates updated

## Version Information

- **SDK Version:** 0.1.0-SNAPSHOT
- **Change Date:** 2026-01-14
- **Change Type:** Breaking Change (Major Version)
