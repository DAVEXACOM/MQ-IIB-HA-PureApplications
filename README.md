# MQ-IIB-HA-PureApplications

IBM MQ v8.0.0.4 and IBM Integration Bus v10.0.0.3+ High availability patterns for IBM Pure Application Systems

Description

This collateral features 2 IBM Pure Application Systems patterns for delivering IBM MQ and IBM Integration Bus (IIB) high availability on IBM Pure Application Systems.

The first pattern features IIB Primary and Standby multi-instance nodes to achieve high availability.
The second pattern features IIB Standalone nodes using MQ Client Connection Definition Table (CCDT) to resolve multi-instance primary and standby queue managers.

I have built the first pattern out leveraging IBM GPFS as the shared file system (shared service on PureAPP) and the second leveraging an NFSv4 server node. I chose to do this for demonstration purposes mainly, there is no reason why pattern 1 cannot be reconfigured to use NFS and pattern 2 GPFS.

Both patterns feature the following.

4 MQ Client only nodes for housing client applications that are set up via CCDT to connect to.....
2 MQ Gateway Queue Managers each with a mulit-instance standby idle partner that are in an MQ cluster with...
2 MQ Application (or backoffice) Queue Managers each with a multi-instance standby idle partner that is serviced by...
  Pattern 1: 2 IIB Primary Nodes locally connected to the MQ Application Queue Managers each with an IIB Standby node
  Pattern 2: 2 IIB Stand alone nodes client connect to the MQ Application Queue Managers via a CCDT. Both IIB nodes can service                both MQ Application Queue Managers and their standby idle nodes.
  
Both patterns use script packages that are written to pick up the IP Address (hostnames) of all the nodes in the pattern and use the hostnames to configure MQ and IIB such that all MQ and IIB connections between nodes are resolved at instantiation time. 
When the pattern is started all the MQ channels start and the nodes come up in a fully connected load balancing MQ Cluster with "loop back" message flows running IIB to service the Application Queue Managers and the MQ Sample applications in the MQ Client only nodes can be used to drive traffic to the MQ Gateway queue managers with no additional set up.

GPFS_HA_CollateralMQ8004_IIB10003.zip - contains the pattern export, all script packages plus full pattern documentation and setup and demo documentation for the IIB Prim/Standby on GPFS.

NFS_HA_CollateralMQ8004_IIB10003.zip - contains the pattern export, all script packages plus full pattern documentation and setup and demo documentation for the IIB Client connect via CCDT on NFS.


