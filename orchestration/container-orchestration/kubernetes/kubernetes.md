# Kubernetes Overview

## Microservices and monoliths

### Monoliths

**Monolith application**: Layers of features and redundant logic translated into thousands of lines
of code, written in a single, not so modern programming language, based on outdated software
architecture patterns and principles.

Monolith challenges:

- Has to run on a single system, which has to satisfy its compute, memory, storage, and networking
  requirements.
- The hardware is complex and very expensive.
- Sometimes it is challenging to maintain.
- Scaling of features is near impossible and expensive.
- Downtime in inevitable during patching.

### Microservices

**Microservices**: Performs a specific business function; when combined, comprise an entire
application.

Microservice advantages:

- Can be deployed individually on separate servers and with fewer resources.
- Only uses what it needs (reduces costs).
- Written in a modern programming language.
- Flexible with what hardware it can run on.
- Scalable at an individual level.
- Seamless upgrades and patching.
- Less downtime (or none).
- Allows businesses to be more productive and cost-effective.

### Path from monolith to microservices

Big bang vs. incremental refactoring:

- Big bang approach focuses all efforts with the refactoring of the monolith.
- Incremental refactoring approach guarantees that new features are microservices that can still
  communicate with the monolith without being included in its codebase.

Refactoring challenges:

- Poor refactoring candidates include:
    - Legacy applications (e.g., written in COBOL or Assembler)
    - Applications tightly coupled with data stores
- Keep all decoupled microservices healthy to ensure resiliency.
- Choosing runtimes:
    - Different libraries and modules often conflict with one another, forcing microservices to run
      on separate VMs or bare metal servers.
    - This is not a very economical usage of resources.  Additionally, each underlying OS also
      consumes resources that could be saved.

## Container orchestration

### What are containers?

**Containers** are an application-centric method to deliver high-performing, scalable applications
on any infrastructure of your choice.  Containers are best suited to deliver microservices by 
offering isolated virtual environments.  They run container images, which bundles the
application along with its runtime, libraries, and dependencies, and represents the source of a
container deployed to offer an isolated executable environment for the application.  Containers can
be deployed on many platforms, such as workstations, VMs, and public clouds.                  

### What is container orchestration?

When migrating from Dev to QA and Production environments, specific requirements need to be met:

- Fault-tolerance
- On-demand scalability
- Optimal resource usage
- Auto-discovery to automatically discover and communicate with each other
- Accessibility from the outside world
- Seamless updates and rollbacks without downtime

**Container orchestrators** are tools which group systems together to form clusters where
containers' deployment and management is automated at scale while meeting the requirements mentioned
above.

Example of container orchestrators include:

- Amazon Elastic Container Services (ECS)
- Azure Container Instances
- Azure Service Fabric
- Kubernetes
- Nomad
- Marathon
- Docker Swarm

Orchestrators make it much easier for users to manage hundreds and thousands of containers.  Most
container orchestrators can:

- Groups hosts together while creating a cluster.
- Schedule containers to run on hosts in the cluster based on resource availability.
- Enable containers in a cluster to communicate with each other regardless of the host they are
  deployed to in the cluster.
- Bind containers and storage resources.
- Group sets of similar containers and bind them to load-balancing constructs to simplify access to
  containerized applications by creating an interface, a level of abstraction between the containers
  and the client.
- Manage and optimize resource usage.
- Allow for implementation of policies to secure access to applications running inside containers.

Most container orchestrators can be deployed on bare metal VMs, on-prem, and on public and hybrid
clouds.  There are turnkey solutions that allow Kubernetes to be installed with a few commands on
cloud IaaS, such as GCE and AWS EC2.  There is also a managed Container-Orchestrator-as-a-Service,
more specifically Kubernetes-as-a-Service, which are offered and hosted by the major cloud
providers.

## Kubernetes

### What is Kubernetes?

> "Kubernetes is an open-source system for automating deployment, scaling, and management of
> containerized applications."

**Kubernetes** comes from a Greek word that means *helmsman* or *ship pilot*.  Kubernetes is also
referred to as **k8s** (pronounced Kate's).  The project is inspired by the Google Borg system,
which is Google's internal container and workload orchestrator.  Kubernetes was started by Google,
who then donated it to the Cloud Native Computing Foundation (CNCF).

### From Borg to Kubernetes

> "Google's Borg system is a cluster manager that runs hundreds of thousands of jobs, from many
> thousands of different applications, across a number of clusters each with up to tens of thousands
> of machines."

Several features/objects of Kubernetes that can be traced back to Borg are:

- API servers
- Pods
- IP-per-Pod
- Services
- Labels

### Kubernetes features

- **Automatic bin packing**: Kubernetes automatically schedules containers based on resource needs
  and constraints, to maximize utilization without sacrificing availability.
- **Designed for extensibility**: A Kubernetes cluster can be extended with new custom features
  without modifying the upstream source code.
- **Self-healing**: Kubernetes automatically replaces and reschedules containers from failed nodes.
  It terminates and then restarts containers that become unresponsive to health checks, based on
  existing rules/policy.  It also prevents traffic from being routed to unresponsive containers.
- **Horizontal scaling**: With Kubernetes, applications are scaled manually or automatically based
  on CPU or custom metrics utilization.
- **Service discovery and load balancing**: Containers receive IP addresses from Kubernetes, while
  it assigns a single DNS name to a set of containers to aid in load balancing requests across the
  containers of the set.
- **Automated rollouts and rollbacks**: Kubernetes seamlessly rolls out and rolls back application
  updates and configuration changes, constantly monitoring the application's health to prevent any
  downtime.
- **Secret and configuration management**: Kubernetes manages sensitive data and configuration
  details for an application separately from the container image, in order to avoid a rebuild of the
  respective image.  Secrets consists of sensitive/confidential information passed to the
  application without revealing the sensitive content to the stack configuration, like on GitHub.
- **Storage orchestration**: Kubernetes automatically mounts software-defined storage (SDS)
  solutions to containers from local storage, external cloud providers, distributed storage, or
  network storage systems.
- **Batch execution**: Kubernetes supports batch execution, long-running jobs, and replaces failed
  containers.
- **IPv4/IPv6 dual-stack**: Kubernetes supports both IPv4 and IPv6 addresses.

### Why use Kubernetes?

Another of Kubernetes strengths is portability.  It can be deployed in many environments, such as
local or remote VMs, bare metal servers, or in public, private, or hybrid clouds.  Kubernetes is
extensible, and its architecture is modular and pluggable.  Its architecture allows decoupled
microservices patterns.  Kubernetes is supported by a thriving community across the world and has
over 3,200 contributors.

### Cloud Native Computing Foundation (CNCF)

CNCF is one of the largest subprojects hosted by the Linux Foundation, and aims to accelerate the
adoption of containers, microservices, and cloud-native applications.  CNCF hosts a multitude of
projects and provides resources to these projects while they continue to operate independently under
their pre-existing governance structures.  Projects within the CNCF are categorized based on their
maturity level (Sandbox, Incubating, and Graduated).

Popular graduated projects:

- **Kubernetes**: container orchestrator
- **etcd**: distributed key-value store
- **CoreDNS**: DNS server
- **containerd**: container runtime
- **Envoy**: cloud native proxy
- **Fluentd**: for unified logging
- **Harbor**: registry
- **Helm**: package management for Kubernetes
- **Linkerd**: service mesh for Kubernetes
- **Open Policy Agent**: policy engine
- **Prometheus**: monitoring system and time series DB
- **Rook**: cloud-native storage orchestrator for Kubernetes

Key incubating projects:

- **argo**: workflow engine for Kubernetes
- **Buildpacks.io**: builds application images
- **CRI-O**: container runtime
- **Contour**: ingress controller for Kubernetes
- **gRPC**: for remote procedure call (RPC)
- **CNI**: for Linux containers networking
- **flux**: continuous delivery for Kubernetes
- **Knative**: serverless containers in Kubernetes
- **KubeVirt**: Kubernetes-based VM manager
- **Notary**: for data security

### CNCF and Kubernetes

For Kubernetes, the CNCF:

- Provides a neutral home for the Kubernetes trademark and enforces proper usage.
- Provides license scanning of core and vendor code.
- Offers legal guidance on patent and copyright issues.
- Creates and maintains open source learning curriculum, training, and certification for Kubernetes
  and cloud native associates (KCNA), administrators (CKA), application developers (CKAD), and
  security specialists (CKS).
- Manages a software conformance working group.
- Actively markets Kubernetes.
- Supports ad hoc activities.
- Sponsors conferences and meetup events.

## Kubernetes architecture

At a very high level, Kubernetes is a cluster of compute systems categorized by their distinct
roles:

- One or more **control plane** nodes
- One or more **worker** nodes (optional, but recommended)

### Control plane nodes

The **control plane node** provides a running environment for the **control plane agents**
responsible for managing the state of a Kubernetes cluster, and it is the brain behind all
operations inside the cluster.  In order to communicate with the Kubernetes cluster, users send
requests to the control plane via a CLI tool, a Web UI Dashboard, or an API.

It is important to keep the control plane running at all costs.  Losing the control plane may
introduce downtime.  To ensure the control plane's fault tolerance, control plane node replicas can
be added to the cluster, configured in HA mode.  While only one of the nodes is dedicated to
actively managing the cluster, the other control plane nodes stay in sync in case the active one
suddenly goes down.

To persist the Kubernetes cluster's state, all cluster configuration data is saved to a distributed
key-value store which only holds cluster state related data.  The key-value stay may be configured
on the control plane node (stacked topology), or on its dedicated host (external topology) to help
reduce the chances of data store loss by decoupling it from the other control plane agents.

In the stacked topology, HA control plane node replicas ensure the key-value store's resiliency.
However, that is not the case with the external topology, where the dedicated key-value store hosts
have to be separately replicated for HA, a configuration that introduces the need for additional
hardware.

#### Control plane node components

A control plane node runs the following essential components and agents:

- API Server
- Scheduler
- Controller Managers
- Key-Value Data Store

In addition, the control plane node runs:

- Container runtime
- Node agent
- Proxy
- Optional add-ons for cluster-level monitoring and logging

##### API server

All the administrative tasks are coordinated by the **kube-apiserver**, a central control plane
component running on the control plane node.  The API Server intercepts RESTful calls from users,
administrators, developers, operations and external agents, then validates and processes them.
During processing the API Server reads the cluster's state from the key-value store, and after a
call's execution, the resulting state is saved to the store.  The API Server is the only control
plane component to talk to the key-value store.

The API Server is highly configurable and customizable.  It can scale horizontally, but also
supports the addition of custom secondary API Servers, which transforms the primary API server into
a proxy to all secondary API servers, routing incoming RESTful calls to them based on custom-defined
rules.

##### Scheduler

The role of the **kube-scheduler** is to assign new workload objects, such as pods encapsulating
containers, to nodes--typically worker nodes.  During the scheduling process, decisions are made
based on current Kubernetes cluster state and new workload object's requirements.  The scheduler
obtains from the key-value store, via the API server, resource usage data for each worker node in
the cluster.  The scheduler also receives from the API server the new workload object's requirements,
which are part of its configuration data.  Requirements may include constraints that users and
operators set, such as scheduling work on a node labeled with **disk==ssd** key-value pair.  The
scheduler also takes into account Quality of Server (QoS) requirements, data locality, affinity,
anti-affinity, taints, toleration, cluster topology, etc. Once all the cluster data is available,
the scheduling algorithm filters the nodes with predicates to isolate the possible node candidates
which then are scored with priorities in order to select the node that satisfies all the
requirements for hosting the new workload.  The outcome of the decision process is communicated back
to the API Server, which then delegates the workload deployment with other control plane agents.

The scheduler is highly configurable and customizable through scheduling policies, plugins, and
profiles.  Additional custom schedulers are supported.

A scheduler is extremely important and complex in a multi-node Kubernetes cluster.
