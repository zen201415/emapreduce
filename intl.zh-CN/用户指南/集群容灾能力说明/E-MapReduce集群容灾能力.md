# E-MapReduce集群容灾能力 {#concept_ldy_w4j_z2b .concept}

本文将介绍E-MapReduce集群数据容灾和服务容灾能力。

## 数据容灾 {#section_bzh_y4j_z2b .section}

Hadoop分布式文件系统\(HDFS\)将每一个文件的数据进行分块存储，同时每一个数据块又保存有多个副本\(系统默认为每一个数据块存放3个副本\),尽量保证这些数据块副本分布在不同的机架之上（在大多数情况下，副本系数是3，HDFS的存放策略是将一个副本存放在本地机架节点上，一个副本存放在同一个机架的另一个节点上，最后一个副本放在不同机架的节点上）。

HDFS会定期扫描数据副本，若发现数据副本发生丢失，则会快速的进行数据的复制以保证副本的数量。若发现节点丢失，则节点上的所有数据也会快速的进行复制恢复。在阿里云上，如果是使用云盘的技术，则在后台每一个云盘都会对应三个数据副本，当其中的任何一个出现问题时，副本数据都会自动进行切换并恢复，以保证数据的可靠性。

Hadoop HDFS是一个经历了长时间考验且具有高可靠性的数据存储系统，已经能够实现海量数据的高可靠性存储。同时基于云上的特性，也可以在OSS等服务上进行数据的额外备份，来达到更高的数据可靠性。

## 服务容灾 {#section_czh_y4j_z2b .section}

Hadoop的核心组件都会进行HA的部署，即有至少2个节点的服务互备，如YARN，HDFS，Hive Server，Hive Meta，以保证在任何时候，其中任何一个服务节点挂掉时，当前的服务节点都能自动的进行切换，保证服务不会受到影响。

