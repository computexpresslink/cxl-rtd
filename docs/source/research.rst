###############
Research Papers
###############

Most of the below are geared towards research in both industry (hyperscalers)
and academia around how to make the best use of CXL memory and the new shift
in memory hierarchy paradigms with tiering and heterogeneous systems becoming
increasingly more relevant.

*************************************************************************************************************
`Demystifying CXL Memory with Genuine CXL-Ready Systems and Devices <https://arxiv.org/pdf/2303.15375.pdf>`_
*************************************************************************************************************
March 2023

TODO (key observations)

****************************************************************************************************
`Pond: CXL-Based Memory Pooling Systems for Cloud Platforms <https://arxiv.org/pdf/2303.15375.pdf>`_
****************************************************************************************************
October 2022

TODO (key observations)

*******************************************************************************************************
`TPP: Transparent Page Placement for CXL-Enabled Tiered Memory <https://arxiv.org/pdf/2206.02878.pdf>`_
*******************************************************************************************************
June 2022 - `kernel discussion/patches <https://lwn.net/Articles/876993/>`_

TODO (key observations)

*****************************************************************************************************
`TMO: transparent memory offloading in datacenters <https://dl.acm.org/doi/10.1145/3503222.3507731>`_
*****************************************************************************************************
ASPLOS22, Febuary 2022.

FB notices that there is a lot of over provisioning of DRAM.
Applications use a lot of virtual memory that is backed by DRAM but
significant amounts of the VM are not used often. Facebook found ways
to identify these pages and then swapped them onto an SSD proactively.
They also modified page reclaim (which does page cache writeback and
swapping) to favor swapping when using a SSD. They are interested in
CXL since they could potentially move colder memory to the CXL device.

First the novelty of the approach; PSI better captures the semantics
about how much a workload is affected by resource shortage, in this
case fast memory - this goes beyond the pages and numa distance
currently heavily used in the kernel. And it leverages memory cgroups
(something used a lot by big tech companies) for introducing proactive
reclaim from userspace and offload cold pages to a slower tier,
instead of relying on hitting memory pressure for the migration. I
also see this benefiting cases of memory pressure because the LRU list
will be better because of any previous proactive reclaim.

Secondly, TMO is being used as a flagship example for changing
upstream Linux kernel reclaim semantics (kswapd and direct reclaim).
The memcg reclaim effort from above is ready for upstream, at least
the beginning conceptual layout: [PATCH resend] memcg: introduce
per-memcg reclaim interface - Yosry Ahmed (kernel.org). These are the
early stages and open the door for maturing memory tiering in Linux.
This is particularly important because while currently the kernel
mostly thinks about only one slower memory tier (pmem), but CXL will
soon add more complexity to this, with multiple tiers of memory. For
example, some things that still need to be defined (and are being
defined):


TODO (key observations)

*****************************************************************************************************************************************************
`Exploring the Design Space of Page Management for Multi-Tiered Memory Systems <https://www.usenix.org/conference/atc21/presentation/kim-jonghyeon>`_
*****************************************************************************************************************************************************
USENIX ATC21, July 2021.

TODO (key observations)
