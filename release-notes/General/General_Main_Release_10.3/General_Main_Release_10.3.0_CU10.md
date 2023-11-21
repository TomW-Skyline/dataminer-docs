---
uid: General_Main_Release_10.3.0_CU10
---

# General Main Release 10.3.0 CU10 – Preview

> [!IMPORTANT]
> We are still working on this release. Some release notes may still be modified or moved to a later release. Check back soon for updates!

> [!TIP]
> For information on how to upgrade DataMiner, see [Upgrading a DataMiner Agent](xref:Upgrading_a_DataMiner_Agent).

### Enhancements

#### Elasticsearch/OpenSearch: Enhanced log entry when creating a custom data storage fails [ID_26965]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

When an attempt to create a custom data storage fails, the log entry will now also mention the data storage type.

Former log entry:

`Cannot create a custom data table for Elastic when Elastic is not active.`

New log entry:

`Cannot create a custom data table for {typeof(T)} in Elastic when Elastic is not active.`

#### New BPA test 'Check Cluster SLNet Connections' [ID_37110]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

When run on a particular agent in a DataMiner System, this new BPA test will trigger a local test on each agent in the DMS that will

- check the connections between the different DMAs and between the DMAs in Failover setups, and
- report any communication problems.

For more information, see [Check Cluster SLNet Connections](xref:BPA_Check_Cluster_SLNet_Connections).

#### Security enhancements [ID_37641]

<!-- 37641: MR 10.2.0 [CU22]/10.3.0 [CU10] - FR 10.4.1 -->

A number of security enhancements have been made.

#### SLAnalytics - Behavioral anomaly detection: Flatline suggestion events will now automatically be cleared after a set amount of time [ID_37716]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

Similar to other types of anomaly suggestion events, flatline suggestion events will now also be cleared automatically after a set amount of time.

> [!NOTE]
> Flatline alarms stay open until the flatline in question disappears or SLAnalytics is restarted.

#### Protocols: Buffer for SNMP responses now has a dynamic size [ID_37824]

<!-- MR 10.2.0 [CU22]/10.3.0 [CU10] - FR 10.4.1 -->

Up to now, when an SNMP response was received, a buffer with a fixed size of 10240 characters was used to translate the response to the requested format (e.g. OctetStringUTF8). When the response was larger that 10240 characters, it was cut off.

From now on, the buffer will have a dynamic size. This allow larger responses to be processed, and will also make sure that less memory has to be reserved when smaller responses are received.

### Fixes

#### DELT: Trend data missing in DELT package after exporting tables with primary keys of type string [ID_37664]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

When you exported tables of which the primary keys were of type string, the DELT export package would incorrectly not contain any trend data.

#### Attempt to update a deleted service would incorrectly cause that service to re-appear [ID_37679]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

In some rare cases, if an attempt was made to update a service that had just been deleted, the service could re-appear.

Additional logging has now been added to allow better tracing of errors that occur while creating or updating services.

#### Problem with remote clients after restarting a DMA in a gRPC-only cluster [ID_37726]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

When a DataMiner System was configured to use gRPC connections only (i.e. when *EnableDotNetRemoting* was set to false on all agents), in some cases, remote clients would not get properly registered with SLDataMiner after restarting a DataMiner Agent. This would cause remote requests to fail if they had to be handled by SLDataMiner on the DataMiner Agent that was restarted.

#### SLAnalytics: Problem when the alarm repository was not available at startup [ID_37782]

<!-- MR 10.2.0 [CU22]/10.3.0 [CU10] - FR 10.4.1 -->

In some cases, an error could occur in SLAnalytics when it was not able to connect to the alarm repository at startup.

#### Entire SNMPv3 response would be discarded when one or more cells contained 'no such instance' [ID_37815]

<!-- MR 10.2.0 [CU22]/10.3.0 [CU10] - FR 10.4.1 -->

When a table was polled via SNMPv3 and the response included a cell that contained *no such instance*, the table would not get populated with the values that were received. Instead, the entire result set would be discarded.

#### Cassandra Cluster: Failover setups would incorrectly report errors when the cluster status was yellow [ID_37868]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

When a Cassandra Cluster was in a yellow state because a number of nodes were down, up to now, Failover setups within the system would incorrectly report errors.

From now on, Failover setups within the system will only report errors if the Cassandra Cluster is in a red state.

#### SLAutomation: Problem when deleting an Automation script dummy that had already been deleted [ID_37907]

<!-- MR 10.3.0 [CU10] - FR 10.4.1 -->

In some rare cases, it would incorrectly be possible to delete an Automation script dummy that had already been deleted, causing an error to occur in SLAutomation.