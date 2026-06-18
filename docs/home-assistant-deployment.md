# Home Assistant Deployment

## Overview
- Deployed: June 17, 2026
- Namespace: `home-assistant`
- Persistent Storage: Yes (10Gi via Local Path)

## Access
- URL: `http://<any-node-ip>:30123` (e.g. http://192.168.4.43:30123)

## Key Learnings
- Used NodePort for easy access
- Affinity rule to prefer worker nodes
- Persistent storage for config and history

## Future Improvements
- Add Philips Hue integration
- Add Zigbee2MQTT for more devices
