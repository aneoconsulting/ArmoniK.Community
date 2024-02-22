# ArmoniK Load Balancer

## Problem

ArmoniK using a single database, queue and object storage, it is hard to make it scale. Distributed Object Storage is simple, but distributed database and queue are much more complex to setup.

A simple alternative is to have multiple isolated clusters, with their own database, queue, and object storage. To make such a design transparent and easy to work with, an ArmoniK Load Balancer would be needed.

Such a Load Balancer would understand the ArmoniK concepts and forwards user requests based on ArmoniK data like the session ID.