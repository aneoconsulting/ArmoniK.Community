# ArmoniK Load Balancer

## Problem

ArmoniK using a single database, queue and object storage, it is hard to make it scale. Distributed Object Storage is simple, but distributed database and queue are much more complex to setup.

A simple alternative is to have multiple isolated clusters, with their own database, queue, and object storage. To make such a design transparent and easy to work with, an ArmoniK Load Balancer would be needed.

Such a Load Balancer would understand the ArmoniK concepts and forwards user requests based on ArmoniK data like the session ID.

## solution overview 

An ArmoniK Load Balancer would be an external service that would serve ArmoniK API in gRPC and redirect them to a cluster.
Upon Session creation, a single cluster is assigned to the session, chosen by the implementation. Afterwards, all requests targeting the session will be redirected to its assigned cluster.
This binding enables to easily keep track of the tasks and data within a session, even if more tasks and data are created from the workers.

No additional API is required, and few adjustments are required infrastructure wise. The ingress in front of the actual cluster should accept authentication header from the load balancer itself, or the load balancer being an authenticated user of the cluster that is able to impersonate any user of the cluster.

The Load Balancer could scale to many servers without issues, especially if they do not need a database.

### Database-less

The simplest design would be to compute deterministcally the cluster where to send the session by computing a hash of the seasion ID.
While this would enable infinite scaling in theory, it comes with a group of issues not that easy to solve.

When the session is created, the cluster must be chosen before the session ID is known. A solution to this problem would be to add an RPC to create a session with a specific session ID and let the Load Balancer generate this ID before choosing a cluster.

Some RPCs do not have the session ID in the request message which would make it hard to get the right cluster. A possible aolution to this is to request the data on all clusters, and cache which result is bound to which session. When the client request the creation of a result, the link between the result and its session could also be recorded in this cache. Apart from Load Balancer booting, this would limit the number of time where the load balancer need to request all clusters. Another solution would be to add the session ID to all requests in the API (see: AEP-xxxxxx)

If the number of clusters change over time, how one could compute to which cluster is bound a session ID is unclear. Moving sessions between clusters to rebalance the distributed hash table does not seem possible. Of course, this problem does not exist if the clusters are static.

### with database

To work around the issues related to absence of a database, we can add a database to the load balancers to record the links between the sessions and the clusters. In particular, there is no need to know the session ID beforehand when creating the session.