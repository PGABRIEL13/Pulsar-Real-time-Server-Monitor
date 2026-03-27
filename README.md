# Pulsar — Real-Time Server Monitor

> A real-time infrastructure monitoring dashboard with live metrics, Canvas-rendered charts, and animated gauge dials. No chart libraries. No dependencies.

![HTML](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![Canvas API](https://img.shields.io/badge/Canvas_API-FF6384?style=flat)
![WebSocket Ready](https://img.shields.io/badge/WebSocket_Ready-010101?style=flat&logo=socketdotio&logoColor=white)

---

## Overview

Pulsar is a production-style infrastructure monitoring dashboard. All charts and gauges are rendered using the raw **HTML5 Canvas API** — no Chart.js, no D3, no external chart libraries. The build uses realistic simulated data with smooth interpolation; connect it to a real WebSocket or REST polling endpoint to monitor actual servers.

## Metrics Tracked

| Metric | Description | Update Rate |
|--------|-------------|-------------|
| CPU Usage | Percentage across all cores | 1.5s |
| Memory | GB used out of total (16 GB) | 1.5s |
| Disk I/O | Read/write throughput in MB/s | 1.5s |
| Network | Inbound + outbound in Mbps | 1.5s |
| CPU Temperature | Core temperature in °C | 1.5s |
| Uptime | Days, hours, minutes since boot | 1s |

## Visualizations

| Chart | Description |
|-------|-------------|
| **Timeline** | 60-second rolling line chart for CPU + Memory |
| **Gauge dials** | Animated arc gauges for CPU, Memory, and Disk |
| **Network bars** | 30-second in/out grouped bar chart |
| **Process table** | Live process list with CPU%, Mem%, and status badges |
| **Alert panel** | Color-coded system event log |

## Getting Started

```bash
git clone https://github.com/YOUR_USERNAME/pulsar-monitor.git
cd pulsar-monitor
open index.html
```

## Connecting to a Real Backend

Replace the `tick()` simulation with a WebSocket listener:

```javascript
const ws = new WebSocket('ws://your-server:8080/metrics');

ws.onmessage = ({ data }) => {
  const { cpu, mem, disk, net, temp, uptime } = JSON.parse(data);
  updateMetrics(cpu, mem, disk, net, temp, uptime);
  drawTimeline(cpu, mem);
};
```

### Recommended Backend

```bash
npm install ws systeminformation
```

Use the `systeminformation` package to expose CPU, memory, disk, and network data over a WebSocket on your server.

## File Structure

```
pulsar-monitor/
├── index.html   # Full dashboard (Canvas API charts + UI)
└── README.md
```

## Roadmap

- [ ] WebSocket backend (Node.js + `systeminformation`)
- [ ] Configurable alert thresholds + desktop notifications
- [ ] Multi-server comparison sidebar
- [ ] Historical data persistence (IndexedDB)
- [ ] Data export to CSV
- [ ] Light theme

## License

MIT
