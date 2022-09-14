# mattertool Commands

Typing partial mattertool commands will provide feedback on the commands including extra information on the options available.

## Network Commands

### Create Network

`mattertool startThread`

### Recover Network

To read Thread dataset to recover network (doesn't seem to work):
`mattertool getThreadDataset`

### Commission New Device to Network

To join a new device to the network using BLE (have to specify the nodeid for the new device using `-n` or can only add one device in v0.3.0):
`mattertool bleThread -n 5808`
Where: 
`5808` is the nodeid for the new device

#### On/Off Cluster Commands

To control the on/off cluster for a node:
`mattertool on -n 5808`
`mattertool off -n 5808`
`mattertool toggle -n 5808`
Where: 
`5808` is the nodeid for the light to be controlled

## Access Control

### Read

To read the ACL from a device, useful to figure out the nodeid of the controller (OTBR) but is fixed to `112233`:
`mattertool accesscontrol read acl 5808 0`
Where:
`5808` is the nodeid of the light already in the network
`0` is the endpoint for device information, (where the ACL is held), always `0`

### Write

To write to the ACL in a light, a device will only react to commands from devices that are in its ACL.
``mattertool accesscontrol write acl '[{"fabricIndex": 1, "privilege": 5, "authMode": 2, "subjects": [112233], "targets": null }, {"fabricIndex": 1, "privilege": 3, "authMode": 2, "subjects": [531, 580], "targets": null }]' 5808 0``
Where:
`112233` is the nodeid of the controller (OTBR)
`531` and `580` are the nodeids of the switches
`5808` is the nodeid of the light (where the ACL is being updated)

**Note**: This always replaces the whole ACL table, take care not to lose the controller (OTBR) entry.

## Binding

### Read

To read the binding table from a switch:
`mattertool binding read binding 580 1`
Where:
`580` is the nodeid of the switch
`1` is the application endpoint of the device that holds the bindings

### Write

To write a single entry to the binding table in a switch:
``mattertool binding write binding '[{"fabricIndex": 1, "node": 5808, "endpoint": 1, "cluster":6}]' 580 1``
Where:
`5808` is the nodeid of the light to be bound
`580` is the nodeid of the switch for the binding table entry

To write multiple entries to the binding table in a switch:
``mattertool binding write binding '[{"fabricIndex": 1, "node": 5808, "endpoint": 1, "cluster":6}, {"fabricIndex": 1, "node": 7135, "endpoint": 1, "cluster":6}, {"fabricIndex": 1, "node": 5816, "endpoint": 1, "cluster":6}]' 531 1``
Where:
`5808`, `7135` and `5816` are the nodeids of the lights to be bound
`531` is the nodeid of the switch for the binding table entry

**Note**: This command always replaces the whole binding table.
