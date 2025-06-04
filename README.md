# Status API

A lightweight monitoring API that periodically checks the status of defined hosts (HTTP endpoints and TCP services).

## Features

- Monitors both HTTP endpoints and TCP services
- Automatically checks status at regular intervals (every 2 minutes)
- Tracks response times and uptime history
- Retains metrics history for the past 2 hours
- Simple REST API to access status information
- Web interface for viewing status data
- Persistent storage of host configurations

## Installation

```bash
git clone https://github.com/astrakit/status-api.git
cd status-api
go build
./status-api
```

The server starts on port 8080 by default.

## API Endpoints

- `GET /api/hosts` - Lists all configured hosts with their status
- `GET /api/hosts/{id}` - Get details for a specific host including metrics history
- `POST /api/check` - Manually trigger a status check for all hosts

## Host Configuration

Hosts are configured in the `hosts.json` file which is automatically created when the application first runs. Below is an example configuration:

```json
[
  {
    "id": "2",
    "name": "Development API",
    "type": "http",
    "address": "https://beta.api.astrakit.cc/api/status",
    "is_up": false,
    "response_time_ms": 0,
    "last_checked": "2025-06-04T09:57:13.100976003+02:00"
  },
  {
    "id": "1",
    "name": "Production API",
    "type": "http",
    "address": "https://api.astrakit.cc/api/status",
    "is_up": true,
    "response_time_ms": 77,
    "last_checked": "2025-06-04T09:57:13.17858747+02:00"
  },
  {
    "id": "3",
    "name": "Main website",
    "type": "http",
    "address": "https://astrakit.cc",
    "is_up": true,
    "response_time_ms": 77,
    "last_checked": "2025-06-04T09:57:13.17858747+02:00"
  },
  {
    "id": "4",
    "name": "Database Server",
    "type": "tcp",
    "address": "192.168.1.100",
    "port": 5432,
    "is_up": false,
    "response_time_ms": 5001,
    "last_checked": "2025-06-04T09:57:18.179813645+02:00"
  },
  {
    "id": "5",
    "name": "Redis Server",
    "type": "tcp",
    "address": "localhost",
    "port": 6379,
    "is_up": false,
    "response_time_ms": 0,
    "last_checked": "2025-06-04T09:57:13.100615443+02:00"
  }
]
```

## Host Types

The application supports two types of host monitoring:

- `http`: For monitoring web endpoints (HTTP/HTTPS)
- `tcp`: For monitoring TCP services like databases

### HTTP Hosts
For HTTP hosts, provide:
- `name`: A descriptive name
- `type`: Set to "http"
- `address`: The URL to check

### TCP Hosts
For TCP hosts, provide:
- `name`: A descriptive name
- `type`: Set to "tcp"
- `address`: The hostname or IP address
- `port`: The TCP port number to connect to

## Web Interface

Access the web interface by opening http://localhost:8080/ in your browser.

## Files

- `hosts.json`: Stores the host configuration
- `metrics.json`: Stores historical metrics data (automatically managed)
- `serve.html`: The web interface HTML file

## License

This project is licensed under the BSD 3-Clause License - see the [LICENSE](LICENSE) file for details.
