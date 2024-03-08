# openshift-virtualization-knowledge
My personal center for all things around Red Hat OpenShift Virtualization
Reach me out:
Feel free to contribute.

# Intro OpenShift Virtualization, RHV, OpenStack

All three technologies rely on the same proven and stable technology stack under the hood. What actually changes between them is the top layer - management and orchestration.

![Virt technology Comparison](https://github.com/sqrex/openshift-virtualization-knowledge/blob/f119dec2d42895c2c66014a8dcc3328382907a07/Red%20Hat%20Virt%20solutions.png)

## Why RHV is being EOL and is Red Hat OpenShift a good replacement?

To understand why Red Hat moved out from Red Hat Virtualization to OpenShift Virtualization its critical to understand long term strategy and vision Red Hat is following.
First of all Red Hat’s strategy assumes that majority of workloads will eventually run on containers.
That’s why Red Hat emphasizes not solely relying on virtualization but rather leveraging OpenShift Virtualization, to bridge the gap between traditional virtual machines (VMs) and containerized applications. This approach allows for a seamless long-term migration from VMs to containers, acknowledging that some workloads may be challenging to convert and will have to stay inside VM’s. 
OpenShift Virtualization, integrates virtualization into the OpenShift container platform, offering a unified management plane for both VMs and containers. 

[This integration aims to solve complex IT problems by utilizing container technology while still supporting essential virtualization features. ]

That’s why the main purpose of OpenShift Virtualization is to provide strategic pathway for organizations to transition towards container-centric infrastructure.
Red Hat also continues to support OpenStack for environments where traditional virtualization remains essential like big private cloud platforms.

## Stability, performance and migration approach

If you ask yourself what would be the best fit and use case for Red Hat Virtualization there is no single good answer for it.

If you would like to follow the strategy Red Hat and the market is heading, the best way would be to look at migration plan from application perspective:

This means that you should:

- Create a list of components each applications is build of and how it is running (VM’s, bare metal, containers etc.)
- Create a list of applications and their components that you plan to modernize (into containers)
- Build per application migration and modernization plan
    - Choose which parts of app will be moved as-is VM-to-VM
    - Choose which parts of app will be modernized into container,serverless
- Migrate plan should be done by Application Team supported by technical how-to’s, DevOps/SRE support team. (Dev, DevOps, SRE, Platform Engineers)

This approach will ensure that you follow application centric approach. It will give you additional benefits like moving all applicationcomponents into one unified platform, ability to describe all app components, including VM’s, as code, centralized logging and monitoring capabilities etc.

**Safety first**

I also suggest our clients to follow more safe migration plan to have more time to learn technology, new concepts like GitOps approach to VM management. 

For that purpose it is great idea to start from one of the following approaches:
- utilize OpenShift Virtualization for Dev environments which will allow DevOps, SysOps to learn the technology, how to do proper sizing etc.
- move so called internal, supportive, no-critical VM’s first. It could be your legacy monitoring system, or reporting system used by less critical supportive department. Check SLA for those apps and choose components that can tolerate f.x. 1-2 days of downtimes etc.

I’m not a big fan of starting from dev environments and learning there as very often dev environments are covered by critical SLA. When you have 300+ developers, you don’t want to disrupt their work on new critical business features… right?
If you still want to go the Dev env path, choose small one, focused on one dev team. Let them be your first early adopters and future evangelists.

**Knowledgebase, Articles, Links**

| Name | Description | Link |
| --- | --- | --- |
| Release notes | Great source of knowledge on what new came in |  |
| OpenShift Virtualization for vSphere Admins | Key concepts of OpenShift Virtualization compared to vSphere terminology and architecture  |  |
| Git repo for  template generator | VM templates generator for OpenShift Virtualization based on ansible |  |
|  |  |  |
| YouTube playlist | Up to date list of all Red Hat YouTube videos around OpenShift Virtualization topic |  |
| GitOps approach for VM lifecycle management | Move from traditional VM management into GitOps approach leveraging ArgoCD and RHOV |  |
| Migration tool | Documentation for VM Migration tool. Examples on how to migrate VM from vSphere and other hypervisors |  |

[https://www.redhat.com/rhdc/managed-files/vi-openshift-virtualization-reference-architecture-f31675-202207-en.pdf](https://www.redhat.com/rhdc/managed-files/vi-openshift-virtualization-reference-architecture-f31675-202207-en.pdf)