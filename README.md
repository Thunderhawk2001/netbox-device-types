# NetBox Device-Type-Templates

Dieses Repository enthält YAML-Device-Type-Templates für NetBox.

## Struktur

```
device-types/
└── <manufacturer>/
    └── <model>.yaml
```

## Validierung

Die Templates werden automatisch bei jedem Push validiert:
- **yamllint**: Syntax- und Formatierungs-Checks
- **yamlfmt**: Konsistente Formatierung

### Lokal validieren

```bash
# Installation
pip install yamllint yamlfmt

# Validieren
yamllint -d relaxed device-types/
yamlfmt -dry -formatter=yaml device-types/
```

## Template-Beispiel

```yaml
manufacturer: Dell
model: PowerEdge R670
slug: dell-poweredge-r670
u_height: 1
is_full_depth: true

interfaces:
  - name: eth0
    type: 1000base-t
  - name: eth1
    type: 1000base-t

power-ports:
  - name: PSU 1
    type: iec-60320-c20
  - name: PSU 2
    type: iec-60320-c20
```

## Wichtige Regeln

- **slug**: `^[-a-z0-9_]+$` mit Hersteller-Prä¹¼x (z.B. `dell-poweredge-r670`)
- **label**: max. 64 Zeichen
- **Typwerte**: Immer aus offizieller NetBox-Doku übernehmen (z.B. `8p8c`, `usb-c`, `iec-60320-c20`)
- **rear-ports**: Kein `rj-45`, `rj-11`, `sfp` → stattdessen `8p8c` oder `other`
- **console-ports**: `usb-c` (nicht `usb-type-c`), `usb-micro-ab` für Micro-USB

## Quellen

- [NetBox Device Type Library](https://github.com/netbox-community/devicetype-library)
- [NetBox Interface Models](https://netboxlabs.com/docs/netbox/models/dcim/interface/)
- [NetBox ConsolePort Models](https://netboxlabs.com/docs/netbox/models/dcim/consoleport/)

## Lizenz

MIT License
