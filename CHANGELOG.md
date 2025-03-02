aws-parallelcluster-cookbook CHANGELOG
======================================

This file is used to list changes made in each version of the AWS ParallelCluster cookbook.

2.4.0
-----

**ENHANCEMENTS**
- Add support for EFA on Centos 7, Amazon Linux and Ubuntu 1604
- Add support for Ubuntu in China region `cn-northwest-1`

**CHANGES**
- SGE: changed following parameters in global configuration
  - `max_unheard 00:03:00`: allows a faster reaction in case of faulty nodes
  - `reschedule_unknown 00:00:30`: enables rescheduling of jobs running on failing nodes
  - `qmaster_params ENABLE_FORCED_QDEL_IF_UNKNOWN`: forces job deletion on unresponsive nodes
  - `qmaster_params ENABLE_RESCHEDULE_KILL`: forces rescheduling or killing of jobs running on failing nodes
- Slurm: decrease SlurmdTimeout to 120 seconds to speed up replacement of faulty nodes
- Always use full master FQDN when mounting NFS on compute nodes. This solves some issues occurring with some networking
  setups and custom DNS configurations
- Set soft and hard ulimit on open files to 10000 for all supported OSs
- Pin python `supervisor` version to 3.4.0
- Remove unused `compute_instance_type` from jobwatcher.cfg
- Removed unused `max_queue_size` from sqswatcher.cfg
- Remove double quoting of the post_install args

**BUG FIXES**
- Fix issue that was preventing Torque from being used on Centos 7
- Start node daemons at the end of instance initialization. The time spent for post-install script and node
  initialization is not counted as part of node idletime anymore.
- Fix issue which was causing an additional and invalid EBS mount point to be added in case of multiple EBS
- Install Slurm libpmpi/libpmpi2 that is distributed in a separate package since Slurm 17


2.3.1
-----

**ENHANCEMENTS**
- FSx Lustre - add support in Amazon Linux

**CHANGES**
- Slurm - upgrade to version 18.08.6.2
- Slurm - declare nodes in separate config file and use FUTURE for dummy nodes
- Slurm - set `ReturnToService=1` in scheduler config in order to recover instances that were initially marked as down
  due to a transient issue.
- NVIDIA - update drivers to version 418.56
- CUDA - update toolkit to version 10.0
- Increase default EBS volume size from 15GB to 17GB
- Add `LocalHostname` to `COMPUTE_READY` events
- Pin `future`, `retrying` and `six` packages in Ubuntu 14.04
- Add `stackname` and `max_queue_size` to sqswatcher configuration


2.2.1
-----

**ENHANCEMENTS**
- `FSx Lustre`: add support for FSx Lustre in Centos7. In case of custom AMI, FSx Lustre is
  only supported with Centos 7.5 and Centos 7.6.

**CHANGES**
- `SGE`: allow users to force job deletion
- `Centos7`: use official AMI as the base image when building ParallelCluster AMI

**BUG FIXES**
- `Torque`: wait for scheduler initialization before completing compute node setup
- `EBS`: fix block device conversion to correctly attach ebs nvme volumes
- `Packer`: retrieve `aws-cfn-bootstrap-latest` package from `cn-north-1` in all China regions.
- `RAID`: automatically prepend `/` to `raid_shared_dir` when not specified in cluster config
- `EBS`: remove extra leading `/` when mounting EBS volumes

**TOOLING**
- Add a script to simplify cookbook package upload when using `custom_chef_cookbook` option


2.1.1
-----

- China Regions, cn-north-1 and cn-northwest-1 support

2.1.0
-----

- EFS support
- RAID support

2.0.2
-----

- Fix issue with jq on ubuntu1404 and centos6. Now using version 1.4
- Fix dependency issue with AWS CLI package on ubuntu1404

2.0.0
-----

- Rename CfnCluster to AWS ParallelCluster
- Support multiple EBS Volumes
- Add AWS Batch as a supported scheduler
- Support Custom AMI's


1.6.0
-----

- Add `scaledown_idletime` to nodewatcher config
- Add cookbook recipes for jobwatcher
- Remove publish_pending scripts


1.5.4
-----

- Set SGE Accounting summary to be true, this reports a single accounting record
for a mpi job
- Add option to disable ganglia `extra_json = { "cfncluster" : { "ganglia_enabled" : "no" } }`


1.5.2
-----

- Fix bug that prevented c5d/m5d instances from working
- Set CPU as a consumable resource in slurm config

1.5.1
-----

Major new features/updates:

  - Added parameter to specify custom cfncluster-node package

Bug fixes/minor improvements:

  - Fixed poise-python dependecy issue
  - Poll on EBS Volume attachment status
  - Added more info on failure of pre and post install files
  - Fixed SLURM cron job to publish pending metric

1.4.1
-----

Major new features/updates:

  - Updated to latest cfncluster-node 1.4.3

1.4.0
-----

Major new features/updates:

  - Updated to Amazon Linux 2017.09.1
  - Applied patches to Ubuntu 16.04
  - Applied patches to Ubuntu 14.04
  - Updated to Centos 7.4
  - Upgraded Centos 6 AMI
  - Updated to Nvidia driver 384
  - Updated to CUDA 9
  - Updated to latest cfncluster-node 1.4.2

Bug fixes/minor improvements:

  - Added support for NVMe-based instance store
  - Fixed ganglia plotting issue on ubuntu
  - Fixed slow SLURM scaling times on systemd platforms.

1.3.2
-----
  - Relicensed to Apache License 2.0
  - Updated to Amazon Linux 2017.03
  - Pulled in latest cookbook dependencies
  - Removed Openlava support

1.2.0
-----
- Dougal Ballantyne <dougalb at amazon dot com>
  - Updated to Chef 12.8.1
  - Updated Openlava to 3.1.3
  - Updated SGE to 8.1.9
  - Updated cfncluster-node to 1.1.0
  - Added slots to compute-ready script
  - Updated cookbook dependencies

1.1.0
-----
- Dougal Ballantyne <dougalb at amazon dot com> - Updated to Amazon Linux 2015.09.2 for base AMI

1.0.1
-----
- Dougal Ballantyne <dougalb at amazon dot com>
  - Fix Ganglia rebuild on 2nd run
  - Update to cfncluster-node==1.0.1

1.0.0
-----
- Dougal Ballantyne <dougalb at amazon dot com> - 1.0.0 release of cookbook matching 1.0.0 release of cfncluster.

0.1.0
-----
- Dougal Ballantyne <dougalb at amazon dot com> - Initial release of cfncluster-cookbooks
