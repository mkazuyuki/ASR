# BCDR for on-premises workloads in ECX

This memo is a response to [the article](https://techcommunity.microsoft.com/t5/azure-infrastructure-blog/business-continuity-and-disaster-recovery-for-on-premises/ba-p/4083157) "Business Continuity and Disaster Recovery for on-premises workloads in Microsoft Azure Cloud" from ECX view point.

## Different Types of DR

There are four types of DR strategies.
1. Backup and Restore
2. Cold DR
3. Warm DR
4. Hot DR

**ASR implements Cold DR.**
**ECX implements Warm DR.**

## Onprem to Cloud Disaster Recovery for server based workloads

The same things are required and provided by ECX as by ASR.

1. Assessment and Inventory
1. Azure Subscription Setup
1. Connectivity
1. Data Replication
1. Failover and Failback Planning
1. Network Configuration
1. Application Dependencies
1. Monitoring and Alerting
1. Documentation and Runbooks
1. Testing and Validation

Some of the *ASR architectural components* are implemented in ECX.

- Configuration Server
- ECX Replicator realizes roles of *Master Target Server*, *Process Server*, and *Azure Site Recovery Replication*.

## In case of ECX: ASR Architectural components

- On-Premises Infrastructure
- Azure Subscription
- ECX provides the components for Monitoring, Failover ad Failback, Replication, Configuration

## In case of ECX: Key points for choosing ASR as your DR solution

- Need to maintain the infrastructure for the DR site while they are not in use, hence we end up requiring cost and maintenance. When the application data is replicating to Azure, you are required the cost of monitoring, patching, and maintaining an on-premises disaster recovery infrastructure by filling the need to build or maintain a secondary datacenter. These datacenters come with an influx of costs, from lengthy contracts to expensive network links.

- There are one and three years contracts for ECX on Azure. There is the option that the cost is based on consumption. Adding to an option of expensive secondary data centers, you will have another option to pay for what you use.

- One requirement of any successful DR tool is accessibility, with ECX, you can replicate, recover, and conduct failover testing from the ECX WebUI. This allows a straightforward method of testing of applications and services during a DR drill for production workloads and end-users.

- ECX allows you to easily comply with industry regulations such as ISO 27001 by enabling Site Recovery between separate regions. You can meet compliance requirements by ensuring that all metadata that is needed to enable and orchestrate replication and failover remains within that region's geographic boundary.

- Easy DR Drills for the compliance auditing report submission. With ECX as your DR solution, you can easily run the DR Drills including the production and the DR site. DR Drill is initiated as failover on dummy failure and it simulates failure detection by monitoring process to validate the DR replication and workload functionality.

## In case of ECX: considerations to keep in mind while designing the ASR as DR solution

- It is recommended to have the management layer up and running as ~~Hot or~~ warm DR in the DR site (i.e. ~~databases,~~ Domain controllers, MFA, RDS servers etc.)
- The best practice is to have the network for the DR site setup and keep it in active or passive mode whatever works for the organization as per their practices.

- Always have the application gateway with waf (if needed and recommended for layer 7 protection at https) to be setup in the DR site and keep the Ip addresses defined for the traffic manager profiles. (Try to use ~~a CNAME~~ an ECX DDNS Resource for the DNS entries) so that the automatic DNS resolutions can be taken care of in the backend when the DR site ~~is spined up~~ become active. 

- ~~Always refer the support matrix for the workloads and configurations that are recommended to be used with ASR as DR.~~
- ~~Try to have beyond 24-hour retention policy for the critical workloads (ASR now supports up to 15 days retention policy)~~  
  **No need for retention policy. ECX Replicator (synchronous replication) attains no-data-loss for failures (crash consistency).**

- ~~Avoid using fully automated failover while using cold DR strategy to not be caught up with false alarms.~~
- Always monitor the health of the replication and take immediate action to resolve any errors.

## In case of ECX: SLA for Site Recovery

- For each Protected Instance configured for On-Premises-to-On-Premises Failover, we guarantee ~~at least 99.9%~~ 99.999% availability of the Site Recovery service.
- For each Protected Instance configured for On-Premises-to-Azure planned and unplanned Failover, we guarantee a ~~two-hour~~ five-minutes Recovery Time Objective.

## In case of ECX: Workload summary while using ASR for the replication

