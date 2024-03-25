# Business Continuity and Disaster Recovery for on-premises workloads in Microsoft Azure Cloud **and EXPRESSCLUSTER**

In this article, we'll briefly explore how you can effectively utilize Microsoft Azure Cloud services to comprehensively plan and orchestrate your disaster recovery strategy.

> This is the comment to [the article](https://techcommunity.microsoft.com/t5/azure-infrastructure-blog/business-continuity-and-disaster-recovery-for-on-premises/ba-p/4083157) from the view point of EXPRESSCLUSTER.

## What is BCDR

BCDR stands for Business Continuity and Disaster Recovery. It encompasses strategies and plans that businesses put in place to ensure continuous operation and swift recovery in the face of unexpected events or disasters, such as human errors, natural calamities, cyberattacks, or equipment failures. BCDR includes measures like data backup, redundancy, alternate communication channels, and recovery protocols to minimize downtime, protect valuable assets, and maintain business operations even during challenging circumstances.

## Why it's crucial for the organizations to must have a fully functional BCDR strategy and solution in place in this fast-paced digital Era

- Minimize Downtime: Keep operations running smoothly during disasters or system failures.
- Protect Data: Safeguard valuable information through regular backups.
- Ensure Continuity: Maintain critical business functions and services without interruption.
- Regulatory Compliance: Adhere to industry regulations and standards for data protection.
- Risk Mitigation: Identify and address potential threats to IT infrastructure.
- Business Reputation: Safeguard against damage to reputation and stability

## Different Types of DR

There are several types of Disaster Recovery (DR) strategies that organizations can implement based on their specific needs and requirements:

1. Backup and Restore
   - This involves regularly backing up data to a secondary storage location and restoring it in case of data loss or corruption. It's typically used for non-critical data and applications with longer recovery time objectives (RTOs) and recovery point objectives (RPOs).
2. Cold DR
   - Cold Disaster Recovery (DR) in the cloud involves storing/replicating primary site data and infrastructure configurations in a dormant state, usually in an offline or powered-off state, until they're required for recovery. Unlike hot DR, where resources are continuously running and ready for immediate failover, cold DR relies on manual intervention (until and unless fully automated with scripts and logics) to activate resources and restore operations in the event of a disaster. This typically results in longer recovery times as resources need to be provisioned, data needs to be restored, and systems need to be brought online. Cold DR is often chosen for its cost-effectiveness and suitability for less critical workloads, where longer downtime is acceptable in exchange for lower operational costs.
3. Warm DR
   - A Warm Disaster Recovery (DR) in the cloud is an intermediate approach between cold and hot DR. In a warm DR setup, standby resources are partially active, meaning they're provisioned and configured but not actively processing workloads. These resources are in a semi-dormant state, ready to be quickly activated and brought online when needed. This allows for faster recovery times compared to cold DR since resources don't need to be fully provisioned from scratch. However, warm DR may still require manual intervention or automation to fully transition to operational status, resulting in a slightly longer recovery time compared to hot DR. Warm DR strikes a balance between cost-effectiveness and recovery speed, making it suitable for workloads that require a quicker recovery but can tolerate a short downtime window.

4. Hot DR
   - Hot Disaster Recovery (DR) in the cloud is the highest level of readiness for disaster scenarios. In a hot DR setup, standby resources are fully active and running in parallel with primary production systems, constantly synchronized and ready to take over instantly in the event of a disaster. This involves real-time or near-real-time replication of data and configurations to the standby environment. When a disaster occurs, failover to the hot standby resources is automatic and seamless, with minimal to no interruption in service. Hot DR offers the fastest recovery times and highest level of availability but comes at a higher cost due to the continuous operation of redundant resources. It's typically used for mission-critical workloads where even the slightest downtime is unacceptable.

> Typically ASR implements Cold DR, and  
> EXPRESSCLUSTER implements Warm DR.

## Onprem to Cloud Disaster Recovery for server based workloads

Planning a BCDR (Business Continuity and Disaster Recovery) strategy from on-premises to Azure involves several technical steps

> The same things are required and provided by ECX as by ASR.

1. Assessment and Inventory
   - Identify critical on-premises systems, applications, and data.
   - Assess dependencies and interconnections between different components.
   - Define the compliance and technical requirement of the RTO (RTO, or Recovery Time Objective, is the maximum acceptable duration of time within which a business process or service must be restored after a disruption or disaster occurs. It represents the target time frame for recovering from a downtime event and resuming normal operations) & RPO (RPO, or Recovery Point Objective, refers to the maximum acceptable amount of data loss that a business can tolerate after a disruption or disaster occurs. It represents the point in time to which data must be recovered in order to resume normal operations, indicating the acceptable data loss window)
   - Design the DR architecture based on the assessment and RTO, RPO Requirement of the organization.
   - Seismic Zone (DR Site location to be defined as per the compliance and best practices recommendation)
2. Azure Subscription Setup
   - Create an Azure subscription if you haven't already.
   - Set up the necessary Azure resources, such as Virtual Networks, Storage Accounts, and Virtual Machines, recovery services vaults etc in the desired Azure region.
3. Connectivity
   - Establish connectivity between your on-premises environment and Azure, using technologies like Azure ExpressRoute or VPN Gateway.
4. Data Replication
   - Implement data replication mechanisms to continuously replicate data from on-premises to Azure, such as Azure Site Recovery (ASR), Native replication mechanism for Databases, Domain controllers, rds servers, mfa servers etc or Azure Blob Storage replication.

   > Different from Azure Site Recovery, ECX Replicator implements synchronous data replication mechanisms to replicate data from on-premises to Azure which ensures that there is no loss of data on disasters (no-data-loss).

5. Failover and Failback Planning
   - Define failover and failback procedures, including the sequence of steps to follow during failover and failback events.
   - Test failover and failback procedures to ensure they work as expected and meet recovery time objectives (RTOs) and recovery point objectives (RPOs).

   > ECX ensures RTO less than 5 minutes.  
   > And also ensures no-data-loss, which results in achieving zero Recovery Point Objective (zero-RPO).

6. Network Configuration
   - Configure network settings in Azure to match those of your on-premises environment, including subnets, IP addresses, routing, and security settings.

7. Application Dependencies
   - Identify and address any dependencies or requirements specific to your applications, such as licensing, authentication, or integration with other systems.

8. Monitoring and Alerting
   - Set up monitoring and alerting mechanisms to monitor the health and performance of your BCDR setup in Azure.
   - Configure alerts to notify you of any issues or failures in replication, connectivity, or resource availability.

   > You utilize ECX monitor resources for monitoring and alerting mechanisms.

9. Documentation and Runbooks:
   - Document the BCDR setup, including configuration details, procedures, and contact information.
Create runbooks with step-by-step instructions for executing failover and failback procedures.

10. Testing and Validation
    - Regularly test the BCDR setup to ensure it meets your recovery objectives and performs as expected.
    - Conduct periodic drills and simulations of disaster scenarios to validate the effectiveness of your BCDR strategy.

Major components involved in designing a BCDR solution from onprem to azure for the server based workloads

1. Recovery Services Vaults: Used for backup and Azure Site Recovery.
2. Storage: Required for storing replicated data and other resources.
3. Compute: Necessary for running workloads during failover in warm and hot DR scenarios.
4. Networking Components: Including connectivity solutions like VPN Gateway or Azure ExpressRoute, SDWAN etc.
5. Traffic Manager: Helps in routing traffic to the appropriate resources during failover.
6. Security Components: Such as Web Application Firewall (WAF), Firewall, DDoS protection, Key Vaults, Defender, and API Management for ensuring security during disaster recovery operations

![Major components involved in designing a BCDR solution from onprem to azure for the server based workloads](https://techcommunity.microsoft.com/t5/image/serverpage/image-id/560791i952D44FE997DC56E)

## What is ASR and how it works

In 2018, Azure became the first large public cloud provider to launch a first-class cloud native disaster recovery solution with Azure to Azure Disaster Recovery. Azure Site Recovery is a cloud-based disaster recovery service provided by Microsoft Azure. It enables businesses to replicate and recover virtual machines, physical servers, and workloads from on-premises datacenters to Azure or between Azure regions, ensuring business continuity in the event of a disaster.

## ASR Architectural components

![ASR Architectural components](https://techcommunity.microsoft.com/t5/image/serverpage/image-id/560794i4C174EF5275C54D5)

> ECX provides following except for:
>
> - On-Premises Infrastructure
> - Azure Subscription

## Key points for choosing ASR as your DR solution

- ​​​​​​​No need to maintain the infrastructure for the DR site while they are not in use, hence we end up saving lot of cost and maintenance. When workloads are replicating to Azure, you can reduce the cost of deploying, monitoring, patching, and maintaining an on-premises disaster recovery infrastructure by eliminating the need to build or maintain a costly secondary datacenter. These datacenters come with an influx of costs, from lengthy contracts to expensive network links

  > In use of ECX, you need to maintain the infrastructure for the DR site while they are not in use, hence we end up requiring cost and maintenance. When the application data is replicating to Azure, you are required the cost of monitoring, patching, and maintaining an on-premises disaster recovery infrastructure by filling the need to build or maintain a secondary datacenter. These datacenters come with an influx of costs, from lengthy contracts to expensive network links.

- There are no long-term contracts for ASR, and the cost is based only on consumption. Unlike expensive secondary data centers, you will only pay for what you use

   > There are one and three years contracts for ECX on Azure. There is the option that the cost is based on consumption. Adding to an option of expensive secondary data centers, you will have another option to pay for what you use.

- One requirement of any successful DR tool is accessibility, with ASR, you can replicate, recover, and conduct failover testing directly from the Azure portal. This allows a straightforward method of testing of applications and services during a DR drill without impacting production workloads or end-users

   > One requirement of any successful DR tool is accessibility, with ECX, you can replicate, recover, and conduct failover testing from the ECX WebUI. This allows a straightforward method of testing of applications and services during a DR drill for production workloads and end-users.

- ASR allows you to easily comply with industry regulations such as ISO 27001 by enabling Site Recovery between separate Azure regions. You can meet compliance requirements by ensuring that all metadata that is needed to enable and orchestrate replication and failover remains within that region's geographic boundary

   > ECX allows you the same with ASR.

- Easy DR Drills for the compliance auditing report submission. With ASR as your DR solution, you can easily run the DR Drills without interfering with the production environment or the DR site. Dr Drill is called as Test failover and it can be performed as a sandbox environment to validate the DR replication and workload functionality

   > Easy DR Drills for the compliance auditing report submission. With ECX as your DR solution, you can easily run the DR Drills including the production and the DR site. DR Drill is initiated as failover on *dummy failure* that simulates failure detection by monitoring process to validate the DR replication and workload functionality.

## considerations to keep in mind while designing the ASR as DR solution

- It is recommended to have the management layer up and running as Hot or warm DR in the DR site (i.e. databases, Domain controllers, MFA, RDS servers etc.)

   > It is recommended to have the management layer up and running as warm DR in the DR site. (i.e. Domain controllers, MFA, RDS servers etc.)

- The best practice is to have the network for the DR site setup and keep it in active or passive mode whatever works for the organization as per their practices.
- Always have the application gateway with waf (if needed and recommended for layer 7 protection at https) to be setup in the DR site and keep the Ip addresses defined for the traffic manager profiles. (Try to use a CNAME for the DNS entries) so that the automatic DNS resolutions can be taken care of in the backend when the DR site is spined up.

   > Always have the application gateway with waf (if needed and recommended for layer 7 protection at https) to be setup in the DR site and keep the Ip addresses defined for the traffic manager profiles. (Try to use an ECX DDNS Resource for the DNS entries) so that the automatic DNS resolutions can be taken care of in the backend when the DR site become active.

- Always refer the support matrix for the workloads and configurations that are recommended to be used with ASR as DR.

   > No need when using ECX.

- Try to have beyond 24-hour retention policy for the critical workloads (ASR now supports up to 15 days retention policy)

   > No need for retention policy. ECX Replicator (synchronous replication) attains no-data-loss for failures ensures crash consistency.

- Avoid using fully automated failover while using cold DR strategy to not be caught up with false alarms.

   > ECX is utilized in warm DR strategy.

- Always monitor the health of the replication and take immediate action to resolve any errors.

   > This is the same in the use of ECX.

## SLA for Site Recovery

- For each Protected Instance configured for On-Premises-to-On-Premises Failover, we guarantee at least 99.9% availability of the Site Recovery service.

   > For each Protected Instance configured for On-Premises-to-On-Premises Failover, we guarantee **99.999%** availability of the Site Recovery service.

- For each Protected Instance configured for On-Premises-to-Azure planned and unplanned Failover, we guarantee a two-hour Recovery Time Objective.

   > For each Protected Instance configured for On-Premises-to-Azure planned and unplanned Failover, we guarantee a **five-minutes** Recovery Time Objective.

Please refer below link for the support matrix of ASR

[Support matrix for Azure VM disaster recovery with Azure Site Recovery - Azure Site Recovery | Micro...](https://learn.microsoft.com/en-us/azure/site-recovery/azure-to-azure-support-matrix)

> Please refer to [ECX Getting Started Guide](https://www.nec.com/en/global/prod/expresscluster/en/doc/manual.html) for the support matrix of ECX.

## Workload summary while using ASR for the replication

Site Recovery can replicate any app running on a supported machine. We've partnered with product teams to do additional testing for the apps specified in the following table

| Workload | Replicate Azure VMs to Azure | Replicate Hyper-V VMs to a secondary site | Replicate Hyper-V VMs to Azure | Replicate VMware VMs to Azure |
|--|--|--|--|--|
| Active Directory, DNS | Yes | Yes | Yes | Yes |
| Web apps (IIS, SQL) | Yes | Yes | Yes | Yes |
| System Center Operations Manager | Yes | Yes | Yes | Yes |
| SharePoint | Yes | Yes | Yes | Yes |
| SAP (Replicate SAP site to Azure for non-cluster) | Yes (tested by Microsoft) | Yes (tested by Microsoft) | Yes (tested by Microsoft) | Yes (tested by Microsoft) |
| Exchange (non-DAG) | Yes | Yes | Yes | Yes |
| Remote Desktop/VDI | Yes | Yes | Yes | Yes |
| Linux (operating system and apps) | Yes (tested by Microsoft) | Yes (tested by Microsoft) | Yes (tested by Microsoft) | Yes (tested by Microsoft) |
| Dynamics AX | Yes | Yes | Yes | Yes |
| Windows File Server | Yes | Yes | Yes | Yes |
| Citrix XenApp and XenDesktop | not | N/A | No | No |

## Key inputs to consider for a smooth BCDR strategy

- Conduct a POC for the BCDR architecture and document DR drill outcomes.
- Utilize native replication mechanisms (e.g., log shipping, Always On, Dataguard etc) for DB replications.

   > The native replication mechanism is recommended because ASR replication is asynchronous and lossy.
   > Since ECX Replicator implements synchronous replication, such consideration is not necessary.

- Avoid IP-based hardening for applications and end users.
- Use different IP ranges for the DR Site to prevent conflicts during failover and failback (Many organizations aim to maintain the same IP addresses from the primary site to the DR site, leading to complexities and limitations in failover and failback due to IP range conflicts)

   > This makes DR solutions difficult to implement. In some cases, resolution by DNS cannot be used because its long propagation time makes the SLA difficult to meet, and resolution by IP address is required.

- Employ a mix of DR approaches (cold, warm, hot) based on requirements.
- Schedule DR drills/Actual DR testing every quarter or 6 months to ensure DR functionality.
- Ensure strong networking design architecture for DR site success.
- Plan failback to virtual env only, as ASR enabled replications cannot failback to physical servers.

   > ECX implements failback. The plan becomes more reasonable.

- ASR can complement your existing replication or DR tools if you have already invested and would like to follow a mix approach.
