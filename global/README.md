# Global NTRIP Services

This directory contains YAML definitions for global and multi-continental NTRIP correction services. These services provide worldwide or near-worldwide coverage, distinguishing them from regional or national services.

## Service Coverage Summary

### Government/Research Networks (Free with Registration)

1. **IGS Real-Time Service** (`igs-real-time.yaml`)
   - Provider: International GNSS Service
   - Coverage: Global scientific network
   - Endpoints: products.igs-ip.net:2101, :443
   - Quality: 5-star reliability and accuracy
   - Access: Free registration required
   - Notes: RTCM-SSR format, operated by BKG for IGS

2. **EUREF-IP** (`euref-ip.yaml`)
   - Provider: EUREF Permanent Network
   - Coverage: European region (35°N-71°N, 10°W-40°E)
   - Endpoints: Multiple (euref-ip.net, euref-ip.be, euref-ip.asi.it)
   - Quality: 5-star government network
   - Access: Free registration required
   - Notes: Operated by ROB (Belgium), BKG (Germany), ASI (Italy)

### Community Networks (Free/Open)

3. **RTK2go** (`rtk2go.yaml`)
   - Provider: RTK2go Community
   - Coverage: Global community stations
   - Endpoints: rtk2go.com:2101, :2102
   - Quality: 4-star community network
   - Notes: Worldwide community base stations, ~50 stations

### Commercial Networks (Subscription Required)

4. **Point One Polaris** (`pointone-polaris.yaml`)
   - Provider: Point One Navigation, Inc.
   - Coverage: Global (US, EU, UK, CA, AU)
   - Endpoints: polaris.pointonenav.com:443, :80
   - Stations: 1,400+
   - Quality: 4-star commercial
   - Notes: Free tier available, commercial pricing for production use

5. **Swift Navigation Skylark** (`swift-skylark.yaml`)
   - Provider: Swift Navigation, Inc.
   - Coverage: Global (US, CA, UK, EU, India, AU, Taiwan, Korea, Japan, China)
   - Endpoints: Regional (na/eu/ap).all-freq.skylark.swiftnav.com:2101, :2102
   - Quality: 4-star reliability, 5-star accuracy (1-2cm RTK)
   - Pricing: $29-200/month depending on service tier
   - Notes: ISO 26262 certified (ASIL B), 99.9% SLA

6. **HxGN SmartNet** (`hxgn-smartnet.yaml`)
   - Provider: Hexagon AB (Leica Geosystems)
   - Coverage: Global (5,300+ reference stations)
   - Endpoints: www.smartnetna.com:2101, :443
   - Quality: 4-star reliability, 5-star accuracy (0.8cm horizontal)
   - Notes: World's largest GNSS correction service, multiple service tiers

7. **Topcon TopNET Live** (`topcon-topnet-live.yaml`)
   - Provider: Topcon Positioning Systems, Inc.
   - Coverage: Global (Asia Pacific, Americas, Europe)
   - Endpoints: rtk.topnetlive.com:2101
   - Quality: 4-star commercial network
   - Notes: 30% US coverage growth in 2024, full GNSS constellation support

## Service Quality Ratings

### Reliability Rating (1-5)
- **5**: Government/scientific networks (IGS, EUREF-IP)
- **4**: Commercial networks with SLA (Skylark, SmartNet, TopNET, Polaris) and established community networks (RTK2go)
- **3**: Community networks (variable reliability)
- **2**: Experimental or intermittent services
- **1**: Legacy or unreliable services

### Accuracy Rating (1-5)
- **5**: Professional RTK accuracy (<2cm) - IGS, EUREF-IP, Skylark, SmartNet
- **4**: High-quality RTK (2-5cm) - TopNET, Polaris, RTK2go
- **3**: Standard RTK (5-10cm)
- **2**: DGPS accuracy (sub-meter)
- **1**: Basic positioning

## Network Types

- **government**: Government-operated scientific/research networks
- **commercial**: Commercial subscription services with SLA
- **community**: Community-operated open networks

## Additional Documentation

### Commercial Pricing Information
See `commercial_pricing_notes.yaml` for detailed pricing information including:
- Monthly subscription costs by service tier
- Coverage area pricing differences
- Academic/educational discounts
- Free trial availability
- Enterprise pricing models

### Excluded Services
See `excluded_commercial_services.yaml` for documentation of commercial services that were researched but excluded from the database, including:
- Trimble CenterPoint RTX (satellite-delivered, proprietary protocol)
- Fugro Seastar/Marinestar (marine-focused, L-band primary)
- TerraStar/Veripos (L-band primary)
- John Deere StarFire (proprietary agricultural system)
- Sapcorda SAPA (SPARTN format, not RTCM)
- NRCan CSRS-PPP (post-processing only, not real-time)

## Service Selection Guidance

### For Research/Education
- **IGS Real-Time Service**: Global scientific network, free registration
- **EUREF-IP**: European regional network, free registration
- **RTK2go**: Community network, basic auth

### For Professional Surveying
- **HxGN SmartNet**: Largest global network, highest station density
- **Swift Skylark**: Modern service, ISO 26262 certified
- **Topcon TopNET Live**: Full constellation support, RTK+PPP

### For Autonomous Vehicles/Robotics
- **Swift Skylark**: ISO 26262 certified, 99.9% SLA
- **Point One Polaris**: Optimized for autonomous applications
- **HxGN SmartNet**: Wide coverage, high reliability

### For Construction/Agriculture
- **Topcon TopNET Live**: Industry-specific features
- **HxGN SmartNet**: Machine control integration
- **Swift Skylark**: Multi-tier accuracy options

### For Hobbyist/Testing
- **RTK2go**: Free community network
- **Point One Polaris**: Free tier available
- **Swift Skylark**: Free trials available

## Authentication Requirements

All services require authentication (username/password via HTTP Basic or Digest):
- **Free registration**: IGS Real-Time, EUREF-IP
- **Account creation**: RTK2go (free)
- **Paid subscription**: Skylark, SmartNet, TopNET, Polaris (commercial tiers)

## NTRIP Protocol Support

All services support:
- NTRIP v1.0 (minimum)
- NTRIP v2.0 (most services)
- SSL/TLS connections (most services offer encrypted ports)

Standard ports:
- 2101: Standard NTRIP (unencrypted)
- 2102: NTRIP over TLS
- 443: HTTPS (some services)
- 80: HTTP (some services)

## Geographic Coverage Levels

Services use hierarchical coverage quality ratings (1-5) for different geographic levels:

- **Continental**: Large continental regions
- **Regional**: Multi-country regions
- **National**: Individual countries
- **State**: State/province level
- **Local**: Local/city level

Higher numbers indicate better coverage and station density at that level.

## Last Verification

All service definitions were verified as of 2024-12-01. Service endpoints, pricing, and features may change. Please verify current information with service providers before deployment.

## Contributing

To suggest additions or corrections to global service definitions:
1. Verify service has truly global or multi-continental coverage
2. Confirm NTRIP endpoint accessibility and authentication requirements
3. Document pricing model and subscription requirements
4. Test service availability and quality
5. Submit service YAML following schema.yaml format

For regional services (single country or smaller), use appropriate regional directories (americas/, emea/, apac/, africa/).
