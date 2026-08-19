# Movelo Architecture

## Prototype

The prototype intentionally separates the UI from tracker hardware.

```text
Simulated telemetry
        |
        v
Vehicle state model
        |
        +--> Dashboard
        +--> Live map
        +--> Fuel
        +--> Alerts
        +--> Trips
```

## Production target

```text
GPS103AB
   |
   | Cellular TCP/UDP
   v
Tracker ingestion gateway
   |
   v
Protocol decoder
   |
   +--> Redis/event queue
   |
   +--> PostgreSQL/PostGIS
   |
   v
Alert + trip services
   |
   v
Movelo API / WebSocket
   |
   v
Web / iOS / Android
```

## Design principles

- Device identity is separate from vehicle identity.
- Tracker protocol is isolated behind a normalized telemetry model.
- Mobile clients never communicate directly with trackers.
- Commands are queued, authorized, acknowledged, and audited.
- Immobilization should be designed for safe stationary prevention rather than an abrupt engine shutdown while moving.
