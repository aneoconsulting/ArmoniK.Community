# ArmoniK Load Balancer

## Problem

ArmoniK using a single database, queue and object storage, it is hard to make it scale. Distributed Object Storage is simple, but distributed database and queue are much more complex to setup.

A simple alternative is to have multiple isolated clusters, with their own database, queue, and object storage. To make such a design transparent and easy to work with, an ArmoniK Load Balancer would be needed.

Such a Load Balancer would understand the ArmoniK concepts and forwards user requests based on ArmoniK data like the session ID.

## solution overview 

An ArmoniK Load Balancer would be an external service that would serve ArmoniK API in gRPC and redirect them to a cluster.
Upon Session creation, a single cluster is assigned to the session, chosen by the implementation. Afterwards, all requests targeting the session will be redirected to its assigned cluster.
This binding enables to easily keep track of the tasks and data within a session, even if more tasks and data are created from the workers.

The Load Balancer could scale to many servers without issues, especially if they do not need a database.

### Database-less

The simplest design would be to compute deterministcally the cluster where to send the session by computing a hash of the seasion ID.
While this would enable infinite scaling in theory, it comes with a group of issues not that easy to solve.