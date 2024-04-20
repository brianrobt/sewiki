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
- Downtime is inevitable during patching.

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

> *"Kubernetes is an open-source system for automating deployment, scaling, and management of
> containerized applications."*

**Kubernetes** comes from a Greek word that means *helmsman* or *ship pilot*.  Kubernetes is also
referred to as **k8s** (pronounced Kate's).  The project is inspired by the Google Borg system,
which is Google's internal container and workload orchestrator.  Kubernetes was started by Google,
who then donated it to the Cloud Native Computing Foundation (CNCF).

### From Borg to Kubernetes

> *"Google's Borg system is a cluster manager that runs hundreds of thousands of jobs, from many
> thousands of different applications, across a number of clusters each with up to tens of thousands
> of machines."*

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
  existing rules and policies.  It also prevents traffic from being routed to unresponsive containers.
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
key-value store which only holds data related to the cluster's state.  The key-value store may be configured
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
During processing, the API Server reads the cluster's state from the key-value store, and after a
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

##### Controller Managers

The **controller managers** are components of the control plane node running controllers or operator
processes to regulate the state of the Kubernetes cluster.  Controllers are watch-loop processes
continuously running and comparing the cluster's desired state with its current state.  If there are
any discrepancies in the cluster's state, corrective action is taken until it matches the desired
state.

The **kube-controller-manager** runs controllers or operators responsible to act when nodes become
unavailable, to ensure container pod counts are as expected, and to create endpoints, service accounts,
and API access tokens.

The **cloud-controller-manager** runs controllers or operators responsible to interact with the
underlying cloud infrastructure when nodes become unavailable, to manage storage volumes when
provided by a cloud service, and to manage load balancing and routing.

##### Key-Value Data Store

**etcd** is a strongly consistent, distributed **key-value data store** used to persist a Kubernetes
cluster's state.  New data is written to the data store only by appending to it; data is never
replaced in the data store.  Obsolete data is compacted periodically to minimize the size of the
data store.

Out of all the control plane components, only the API Server is able to communicate with the data store.

etcd's CLI management tool -- **etcdctl** -- provides snapshot save and restore capabilities, which
are useful in Development and learning environments.  However, in Stage and Production environments,
it is extremely important to replicate the data stores in HA mode to ensure cluster configuration
data resiliency.

Some Kubernetes cluster bootstrapping tools, such as **kubeadm**, provision stacked etcd control
plane nodes by default, where the data store runs alongside and shares resources with the other
components on the control plane node.

For data store isolation from the control plane components, bootstrapping can be configured for an
external etcd topology, where the data store is provisioned on a dedicated separate host, thus
reducing the chances of an etcd failure.

Both stacked and external etcd topologies support HA configurations.  etcd is based on the **Raft
Consensus Algorithm**, which allows a collection of machines to work as a coherent group that can
survive the failures of some of its members.  At any given time, one node will be the leader and the
rest will be the followers.  etcd gracefully handles leader elections and can tolerate node failure.

etcd is written in Go, and is also used to store configuration details such as subnets, ConfigMaps,
Secrets, etc.

### Worker nodes

A **worker node** provides a running environment for client applications.  In Kubernetes, the
application containers are encapsulated in Pods, which are controlled by the cluster control plane
agents.  Pods are scheduled on worker nodes.  A Pod is the smallest scheduling work unit in
Kubernetes.  It is a logical collection of one or more containers scheduled together.  The
collection can be started, stopped, or rescheduled as a single unit of work.

In a multi-worker Kubernetes cluster, the network traffic between client users and the containerized
applications deployed in Pods is handled directly by the worker nodes, and is not routed through the
control plane node.

#### Worker node components

A worker node has the following components:

- Container Runtime
- Node Agent - kubelet
- Proxy - kube-proxy
- Add-ons for DNS, Dashboard user interface, cluster-level monitoring and logging

##### Container Runtime

In order to manage a container's lifecycle, Kubernetes requires a **container runtime** on the node
where a Pod and its containers are to be scheduled.  Runtimes are required on all nodes of a
Kubernetes cluster, both control plane and worker nodes.  Kubernetes supports several container
runtimes:

- **CRI-I**: A lightweight container runtime for Kubernetes, supporting **quay.io** and **Docker
  Hub** image registries.
- **containerd**: A simple, robust, and portable container runtime.
- **Docker Engine**: A popular and complex container platform which uses **containerd** as a
  container runtime.
- **Mirantis Container Runtime**: Formerly known as the **Docker Enterprise Edition**.

##### Node Agent - kubelet

The **kubelet** is an agent running on each node, control plane and workers, and communicates with
the control plane.  It receives Pod definitions, primarily from the API server, and interacts with
the container runtime on the node to run containers associated with the Pod.  It also monitors the
health and resources of Pods running containers.

The kubelet connects to container runtimes through a plugin-based interface -- the **Container
Runtime Interface** (CRI).  The CRI consists of protocol buffers, gRPC API, libraries, and
additional specifications and tools.  In order to connect to interchangeable container runtimes,
kubelet uses a **CRI shim**, which is an application that provides an abstraction layer between
kubelet and the container runtime.

The CRI implements two services: **ImageService** and **RuntimeService**.  The ImageService is
responsible for all the image-related operations, while the RuntimeService is responsible for all the
Pod and container-related operations.

##### kubelet - CRI shims

Shims are CRI implementations, interfaces or adapters, specific to each container runtime supported
by Kubernetes.  Some examples of CRI shims include:

- **cri-containerd**: Allows containers to be directly created and managed with containerd at
  kubelet's request.
- **CRI-O**: Enables the use of any Open Container Initiative (OCI) compatible runtime with
  Kubernetes, such as runC.
- **dockershim** and **cri-dockerd**: Before Kubernetes release v1.24, the dockershim allowed
  containers to be created and managed by invoking the Docker Engine and its internal runtime,
  containerd.  Due to Docker Engine's popularity, this shim has been the default interface used by
  kubelet.  However, starting with Kubernetes v1.24, the dockershim is no longer being maintained by
  the Kubernetes project.  As a result, **Docker, Inc.** and **Mirantis** have agreed to introduce
  and maintain a replacement adapter, **cri-dockerd**, that would ensure that the Docker Engine will
  continue to be a container runtime option for Kubernetes, in addition to the Mirantis Container
  Runtime (MCR).  This also ensures that both Docker Engine and MCR follow the same standardized
  integration method as the CRI-compatible runtimes.

##### Proxy - kube-proxy

The **kube-proxy** is the network agent which runs on each node, control plane and workers,
responsible for dynamic updates and maintenance of all networking rules on the node.  It abstracts
the details of Pods and networking and forwards connection requests to the containers in the Pods.

The kube-proxy is responsible for TCP, UDP, and SCTP stream forwarding or random forwarding across a
set of Pod backends of an application, and it implements forwarding rules defined by users through
Service API objects.

##### Add-ons

Add-ons are cluster features and functionality not yet available in Kubernetes, and therefore
implemented through 3rd-party pods and services:

- **DNS**: Cluster DNS is a DNS server required to assign DNS records to Kubernetes objects and
  resources.
- **Dashboard**: A general purpose web-based user interface for cluster management.
- **Monitoring**: Collects cluster-level container metrics and saves them to a central data store.
- **Logging**: Collects cluster-level container logs and saves them to a central log store for
  analysis.

### Networking challenges

Decoupled microservice-based applications rely heavily on networking in order to mimic the
tight-coupling of monoliths.  Kubernetes needs to address a few distinct networking challenges:

- Container-to-Container communication inside Pods.
- Pod-to-Pod communication on the same node and across cluster nodes.
- Service-to-Pod communication within the same namespace and across cluster namespaces.
- External-to-Service communication for clients to access applications in a cluster.

#### Container-to-Container communication inside Pods

Using the host OS's kernel virtualization features, a container runtime creates an isolated network
space for each container it starts.  On Linux, the isolated network space is referred to as a
**network namespace**.  A network namespace can be shared across containers, or with the host OS.

When a grouping of containers defined by a Pod is started, a special infrastructure **Pause
container** is initialized by the Container Runtime for the sole purpose of creating a network
namespace for the Pod.  All additional containers running inside the Pod will share the Pause
container's network namespace so that they can all talk to each other via localhost.

#### Pod-to-Pod communication across nodes

Pods are scheduled on nodes in a nearly unpredictable fashion.  Regardless of their host node, Pods
are expected to be able to communicate with all other Pods in the cluster, and without the
implementation of Network Address Translation (NAT).  This is a fundamental requirement of any
networking implementation in Kubernetes.

The Kubernetes network model aims to reduce complexity by treating Pods as VMs on a network, where
each VM is equipped with a network interface; thus, each Pod receives a unique IP address.  This
model is called "**IP-per-Pod**", and ensures Pod-to-Pod communication.

Containers share the Pod's network namespace and must coordinate port assignments inside the Pod
while being able to communicate with each other on localhost inside the Pod.  Containers are
integrated with the Kubernetes networking model through the **Container Network Interface (CNI)**,
which is supported by CNI plugins.  CNI is a set of specifications and libraries which allow plugins
to configure the networking for containers.  There are a few core plugins, but most CNI plugins are
3rd-party Software Defined Networking (SDN) solutions.  Some of these SDNs offer support for Network
Policies, like Flannel, Weave, and Calico.

The container runtime offloads the IP assignment to CNI, which connects to the underlying configured
plugin, such as Bridge or MACvlan, to get the IP address.  Once the IP address is given by the
plugin, the CNI forwards to back to the requested container runtime.

#### External-to-Pod communication

A successfully deployed containerized application running in Pods inside a Kubernetes cluster may
require accessibility from the outside world.  Kubernetes enables external accessibility through
**Services**, which are complex encapsulations of network routing rule definitions stored in
**iptables** on cluster nodes and implemented by **kube-proxy** agents.  By exposing services to the
external world with kube-proxy, applications become accessible from outside the cluster via a
virtual IP address and port.
