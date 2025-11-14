# Quick Start Guide

Get started with Elli Client in minutes.

## Installation

```bash
pip install elli-client
```

## Basic Usage

### 1. Login and Get Stations

```python
from elli_client import ElliAPIClient

# Create client and login
client = ElliAPIClient()
token = client.login("your.email@example.com", "your_password")

# Get your charging stations
stations = client.get_stations()
for station in stations:
    print(f"Station: {station.name}")
    print(f"  Model: {station.model}")
    print(f"  Firmware: {station.firmware_version}")

# Don't forget to close
client.close()
```

### 2. Using Context Manager (Recommended)

```python
from elli_client import ElliAPIClient

with ElliAPIClient() as client:
    client.login("your.email@example.com", "your_password")

    stations = client.get_stations()
    print(f"Found {len(stations)} station(s)")
    # Automatic cleanup
```

### 3. Check Active Charging

```python
from elli_client import ElliAPIClient

with ElliAPIClient() as client:
    client.login("your.email@example.com", "your_password")

    # Get all sessions with power data
    sessions = client.get_charging_sessions(include_momentary_speed=True)

    # Find active sessions
    active = [s for s in sessions if s.lifecycle_state == "ACTIVE"]

    if active:
        session = active[0]
        kwh = session.energy_consumption_wh / 1000
        watts = session.momentary_charging_speed_watts
        print(f"Currently charging: {kwh:.2f} kWh at {watts} W")
    else:
        print("No active charging")
```

### 4. Get Historical Sessions

```python
from elli_client import ElliAPIClient

with ElliAPIClient() as client:
    client.login("your.email@example.com", "your_password")

    # Get all sessions (without power data for faster response)
    sessions = client.get_charging_sessions(include_momentary_speed=False)

    # Filter completed sessions
    completed = [s for s in sessions if s.end_date_time]

    print(f"Total sessions: {len(completed)}")

    # Calculate total energy
    total_kwh = sum(s.energy_consumption_wh or 0 for s in completed) / 1000
    print(f"Total energy: {total_kwh:.2f} kWh")
```

### 5. Get Station Statistics

```python
from elli_client import ElliAPIClient

with ElliAPIClient() as client:
    client.login("your.email@example.com", "your_password")

    # Get your first station
    stations = client.get_stations()
    station = stations[0]

    # Get accumulated statistics
    stats = client.get_accumulated_charging(station.id)
    print(f"Station: {station.name}")
    print(f"Stats: {stats}")
```

## Common Patterns

### Error Handling

```python
from elli_client import ElliAPIClient

try:
    with ElliAPIClient() as client:
        client.login("your.email@example.com", "your_password")
        stations = client.get_stations()
except ValueError as e:
    print(f"Error: {e}")
```

### Using Environment Variables

For development, you can use a `.env` file:

```bash
# 1. Copy the template
cp .env.template .env

# 2. Edit .env and add your credentials
# ELLI_EMAIL=your.email@example.com
# ELLI_PASSWORD=your_password
```

Then in your code:

```python
import os
from elli_client import ElliAPIClient

# Load from environment variables
email = os.getenv("ELLI_EMAIL")
password = os.getenv("ELLI_PASSWORD")

with ElliAPIClient() as client:
    client.login(email, password)
    stations = client.get_stations()
```

## Next Steps

- **[API Reference](api.md)** - Complete documentation of all methods
- **[GitHub](https://github.com/marcszy91/elli-client)** - Source code and issues

## Need Help?

- Check the [API Reference](api.md) for detailed documentation
- Open an issue on [GitHub](https://github.com/marcszy91/elli-client/issues)
