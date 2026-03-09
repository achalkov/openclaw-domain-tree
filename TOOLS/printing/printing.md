# printing — Network printer configuration

## Purpose
Configuration for printing from the homelab environment.

## Printer: EPSON L3260 Series
- Model: EPSON L3260 Series
- Hostname: `${agent.tools.printing.hostname}`
- IP: `${agent.tools.printing.ip}`
- CUPS queue: `${agent.tools.printing.cups_queue}`
- Default printer on homelab: yes

## Usage
Print command (run on homelab via SSH):
```
lp -d EPSON_L3260_Series <file>
```

## Variables
- `agent.tools.printing.hostname` — `EPSON7E92BB.local`
- `agent.tools.printing.ip` — `192.168.2.35`
- `agent.tools.printing.cups_queue` — `EPSON_L3260_Series`

## Accumulated rules
(empty)
