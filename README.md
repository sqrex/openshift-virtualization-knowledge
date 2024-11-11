# openshift-virtualization-knowledge
My personal center and gathered knowledge around Red Hat OpenShift Virtualization Technology


# OpenShift Virtualization, RHV, OpenStack

All three technologies rely on the same proven and stable technology stack under the hood. What actually changes between them is the top layer - management and orchestration.

![Virt technology Comparison](https://github.com/sqrex/openshift-virtualization-knowledge/blob/ac14e56e9d44e38de9913fc4e5c828b294dca578/Red%20Hat%20Virt%20solutions.png)

## Why RHV is being EOL? Is Red Hat OpenShift a good replacement?

To understand why Red Hat moved out from Red Hat Virtualization to OpenShift Virtualization its critical to understand their long term strategy and vision.
First of all Red Hat’s strategy assumes that majority of workloads will eventually run on containers.
That’s why Red Hat emphasizes not solely relying on virtualization but rather leveraging OpenShift Virtualization, to bridge the gap between traditional virtual machines (VMs) and containerized applications. This approach allows for a seamless long-term migration from VMs to containers, acknowledging that some workloads may be challenging to convert and will have to stay inside VM’s. 
OpenShift Virtualization, integrates virtualization into the OpenShift container platform, offering a unified management plane for both VMs and containers. 

[This integration aims to solve complex IT problems by utilizing container technology while still supporting essential virtualization features.]

That’s why the main purpose of OpenShift Virtualization is to provide strategic pathway for organizations to transition towards container-centric infrastructure.
Red Hat also continues to support OpenStack for environments where traditional virtualization remains essential like big private cloud platforms.

## Stability, performance and migration approach

If you ask me what would be the best fit and use case for Red Hat Virtualization - I would say that there is no single good answer for it.

If you would like to follow the strategy Red Hat and the market is heading, the best way would be to look at migration plan from application perspective, not from hypervisor perspective.

This means that you should:
- Create a list of components each applications is build of and how it is running (VM’s, bare metal, containers etc.)
- Create a list of applications and their components that you plan to modernize (into containers)
- Build per application migration and modernization plan
    - Choose which parts of app will be moved as-is VM-to-VM
    - Choose which parts of app will be modernized into container,serverless
- Migrate plan should be done by Application Team supported by technical how-to’s, DevOps/SRE support team. (Dev, DevOps, SRE, Platform Engineers)

This approach will ensure that you follow application centric approach. It will give you additional benefits like moving all application components into one unified platform, ability to describe all app components, including VM’s, as code, centralized logging and monitoring capabilities etc.


I suggest our clients to follow more safe migration plan to have  time to learn technology and new concepts like GitOps approach to VM management. 

For that purpose it is great idea to start from one of the following approaches:
- utilize OpenShift Virtualization for Dev environments which will allow DevOps, SysOps to learn the technology, how to do proper sizing etc.
- move so called internal, supportive, no-critical VM’s first. It could be your legacy monitoring system, or reporting system used by less critical supportive department. Check SLA for those apps and choose components that can tolerate f.x. 1-2 days of downtimes etc.
- move RHEL workloads (save $$$ on RHEL Subscription costs)

I’m not a big fan of starting from dev environments and learning there as very often dev environments are covered by critical SLA. When you have 300+ developers, you don’t want to disrupt their work on new critical business features… right?
If you still want to go the Dev env path, choose small one, focused on one dev team. Let them be your first early adopters and future evangelists.

## VMWare and OpenShift comparison

### Glossary

| Feature | vSphere | OpenShift Virtualization |
| --- | --- | --- |
| VM Live Migration | vMotion | Live Migration |
| VM Memory overcommit | Yes | Yes |
| Storage Live Migration | Storage vMotion | No functionality |
| Resource rebalancing | Pod eviction policy, descheduler | DRS (Dynamic Resource Scheduling) |
| Storage backend | datastore, vSAN, arrays | PVC through CSI |
| Network backend | vSwitch, DvSwitch, NSX-T | Multus, OpenShiftSDN, nmstate, CNI (partners) |
| Host and VM metrics | vCenter, vROps | OpenShift Metrics,  |


## Knowledgebase, Articles, Links

### Red Hat knowledge sources
| Name | Description | Link |
| --- | --- | --- |
| Release notes | Great source of knowledge on what new came in | [Link](https://docs.openshift.com/container-platform/4.17/virt/release_notes/virt-4-17-release-notes.html) |
| Rerefence Guide | OpenShift Virtualization official Implementation Guide | [Link] (https://access.redhat.com/sites/default/files/attachments/openshift_virtualization_reference_implementation_guide.pdf#page6) |
| OpenShift Virtualization for vSphere Admins | Key concepts of OpenShift Virtualization compared to vSphere terminology and architecture  | [Link](https://www.redhat.com/en/blog/openshift-virtualization-for-vsphere-admins-an-introduction-to-network-configurations) |
| YouTube playlist | Up to date list of all Red Hat YouTube videos around OpenShift Virtualization topic | [Link](https://www.youtube.com/playlist?list=PLaR6Rq6Z4IqeQeTosfoFzTyE_QmWZW6n_) |
| GitOps approach for VM lifecycle management | Move from traditional VM management into GitOps approach leveraging ArgoCD and RHOV | [Link](https://www.redhat.com/en/blog/virtual-machines-as-code-with-openshift-gitops-and-openshift-virtualization) |
| Migration tool | Documentation for VM Migration tool. Examples on how to migrate VM from vSphere and other hypervisors | [Link](https://docs.redhat.com/en/documentation/migration_toolkit_for_virtualization/2.7) |
| Big scale deployment | Performance tests with 3 000 VMs and 21,400 pods running on OpenShift Virtualization | [Link](https://www.redhat.com/rhdc/managed-files/vi-openshift-virtualization-reference-architecture-f31675-202207-en.pdf) |

### External Vendor related documents

| Name | Description | Link |
| --- | --- | --- |
| Lenovo | Reference architecture for OCP 4.13, deployment on Lenovo servers  | [Link](https://lenovopress.lenovo.com/lp0968.pdf) |
| DELL | Design guide for OCP 4.14 deployment on DELL servers | [Link](https://infohub.delltechnologies.com/static/media/client/7phukh/DAM_e55a1069-ee75-43de-8a7d-ac843984caf7.pdf) |
| HPE | Reference architecture for OCP 4.14, deployment on HPE DL servers  | [Link](https://www.hpe.com/psnow/downloadDoc/HPE%20Reference%20Configuration%20for%20Red%20Hat%20OpenShift%20Container%20Platform%204.14%20on%20HPE%20ProLiant%20DL360%20&%20DL380%20Gen11%20servers-a50010318enw.pdf?id=a50010318enw&isFutureVersion=true&ver=&form=false&preview=false&print=&hf=regular&r=&section=&prelaunchSection=&softrollSection=&deepLink=&utm_source=&utm_medium=&utm_campaign=&utm_content=&utm_term=&isLinearized=false&contentDisposition=attachment) |
| HPE | Reference Architecture for OCP 4.15 and OpenShift Virtualization on HPE DL Servers | [Link](https://www.hpe.com/psnow/downloadDoc/HPE%20Reference%20Configuration%20for%20Red%20Hat%20OpenShift%20Virtualization%20on%20HPE%20ProLiant%20DL360%20and%20DL380%20Gen11%20servers%20using%20Red%20Hat%20OpenShift%20Container%20Platform%204.15-a50011012enw.pdf?id=a50011012enw)
| Cisco | Reference architecture for OCP 4.12, deployment on Cisco  | [Link](https://www.cisco.com/c/en/us/td/docs/dcn/aci/containers/installation/openshift-on-baremetal/installing-openshift-4-12-on-baremetal.html) |
| Git repo for  template generator | VM templates generator for OpenShift Virtualization based on ansible | [Link](https://github.com/kubevirt/common-templates?tab=readme-ov-file) |




Feel free to contact me if you are interested in discovery workshops around Red Hat OpenShift technologies.
You can reach me out here: https://www.linkedin.com/in/devops-sre-infrastructure-team-lead-rafal-skora/

Feel free to contribute to this document.