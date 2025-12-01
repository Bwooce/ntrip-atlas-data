# NTRIP Atlas Service Database

Community-maintained database of global NTRIP services for automatic service discovery.

## Overview

This repository contains the service database for [NTRIP Atlas](https://github.com/bruce/ntrip-atlas), providing structured YAML data about NTRIP casters worldwide. The main library repository handles the C library code, while this repository focuses purely on service data.

## Database Structure

```
data/
├── VERSION              # Database version info
├── GLOBAL/             # Worldwide services (RTK2GO, Point One Polaris)
├── EMEA/               # Europe, Middle East, Africa (including South Africa)
├── APAC/               # Asia Pacific region
└── AMER/               # Americas (North & South America)
```

## Current Services

**Database Version**: 20241201.01
**Total Services**: 33
**Geographic Coverage**: 4 regions

### Service List
- **RTK2GO**: Global community network (800+ stations)
- **Point One Polaris**: Commercial global network (1,400+ stations)
- **EUREF-IP**: European government network (BKG/ROB casters)
- **Finland FinnRef**: Finnish government network (47 stations)
- **Massachusetts MaCORS**: US state network (22 stations)
- **Geoscience Australia**: Australian government network

## Contributing

### Adding New Services

1. **Research the service**: Verify it's publicly accessible and stable
2. **Create YAML file**: Follow the schema in existing service files
3. **Validate**: Run `python3 ../ntrip-atlas/tools/validators/service_validator.py --directory data`
4. **Test connectivity**: Ensure the service actually works
5. **Submit PR**: Include documentation of testing performed

### Service Requirements

Services must meet these criteria to be included:
- **Public access**: Either free or with clear registration process
- **Reliable operation**: Service should have good uptime history
- **Accurate coverage**: Geographic boundaries must be verified
- **RTCM compatibility**: Must provide standard RTCM messages
- **Documented authentication**: Clear auth requirements if any

### YAML Schema

Each service file must include:
```yaml
service:
  id: "unique_identifier"           # For credential storage
  provider: "Organization Name"     # Who runs the service
  country: "ISO-3166"              # Country code
  quality:
    reliability_rating: 4          # 1-5 stars based on uptime
    accuracy_rating: 4             # 1-5 stars based on precision
  coverage:
    bounding_box:                  # Conservative geographic limits
      lat_min: -45.0
      lat_max: -10.0
      lon_min: 110.0
      lon_max: 160.0
  endpoints: [...]                 # Connection details
  authentication: [...]            # Auth requirements
```

## Quality Standards

### Service Ratings
- **5 stars**: Government services (GA, NRCan, BKG)
- **4 stars**: Commercial with SLA (Trimble VRS, Leica SmartNet)
- **3 stars**: Reliable community (RTK2go stable stations)
- **2 stars**: Experimental or intermittent services
- **1 star**: Legacy or unreliable services

### Validation Process
All services are automatically validated on every commit:
- YAML schema compliance
- Geographic coordinate validation
- Required field completeness
- Cross-reference consistency

## Versioning

Database versions follow `YYYYMMDD.sequence` format:
- **YYYYMMDD**: Date of last data update
- **sequence**: Incremental number for same-day updates (01, 02, 03...)

Example: `20241130.01` = First update on November 30, 2024

## Licensing

This database is released under [Creative Commons Zero (CC0)](LICENSE-DATA) - effectively public domain. You can use this data for any purpose without attribution requirements.

The goal is to eliminate barriers to global NTRIP service discovery and enable universal precision positioning.

## Integration

This database is designed to work with the [NTRIP Atlas library](https://github.com/bruce/ntrip-atlas):

```c
#include "ntrip_atlas.h"

// Automatic service discovery using this database
ntrip_service_t best_service;
ntrip_atlas_find_best(&best_service, user_lat, user_lon);
```

## Community

- **Issues**: Report data errors or request new services
- **Discussions**: Coordinate with regional NTRIP operators
- **Wiki**: Service-specific notes and regional guidance

## Security Notice

This database contains only publicly documented NTRIP services. No credentials or private access information is stored here. Authentication requirements are documented for transparency only.