Traps provide a way for an agent to send a monitoring station asynchronous notification about conditions that the monitor should know about. The traps that an agent can generate are defined by the MIBs it supports; the number of traps can range from zero to hundreds. To see what traps are defined in any MIB file, search for the term TRAP-TYPE (SMIv1) or NOTIFICATION-TYPE (SMIv2) in the MIB file.



### Understanding Traps

A trap is basically an asynchronous notification sent from an SNMP agent to a network management station. Traps are sent using UDP (port 162) and are therefore unreliable. Traps fall into two categories: generic and enterprise specific. There are seven generic trap number (0-6). 

Table 2-8. Generic traps


| Generic trap name and number | Definition                                                   |
| ---------------------------- | ------------------------------------------------------------ |
| coldStart (0)                | Indicates that the agent has rebooted. All management variables will be reset; specifically, Counters and Gauges will be reset to zero (0). One nice thing about the coldStart trap is that it can be used to determine when new hardware is added to the network. When device is powered on, it sends this trap to its trap destination. If the trap destination is set correctly (i.e., to the IP address of your NMS), the NMS can receive the trap and determine whether it needs to manage the device. |
| warmStart (1)                | Indicates that the agent has reinitialized itself. None of the management variables will be reset. |
| linkDown (2)                 | Sent when an interface on a device goes down. The first variable binding identifies the index in the interfaces table for the interface that went down. |
| linkUp (3)                   | Sent when an interface on a device comes back up. The first variable binding identifies which interface came back up. |
| authenticationFailure (4)    | Indicates that someone has tried to query your agent with an incorrect community string; useful in determining if someone is trying to gain unauthorized access to one of your devices. |
| egpNeighborLoss (5)          | Indicates that an EGP neighbor has gone down.                |
| enterpriseSpecific (6)       | Indicates that the trap is enterprise-specific. SNMP vendors and users define their own traps under the private-enterprise branch of the SMI object tree. To process this trap properly, the NMS has to decode the specific trap number that is part of the SNMP message. |

An enterprise-specific trap is identified by two pieces of information: the enterprise ID of the organization that defined the trap and the specific trap number assigned by that organization. For example, if your enterprise number is 2789, your enterprise ID is 1.3.6.1.4.1.2789, you can define traps with enterprise IDs such as 1.3.6.1.4.1.2789.5000, 1.3.6.1.4.1.2789.5001, and so on.