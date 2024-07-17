This repository contains code and yaml for the Rosen Astro group for use on the [CSU TIDE](tide.sdsu.edu) cluster.

**Namespace name:** sdsu-rosen-astro-group

## Shared Data

The following PVCs (disks) are available in the sdsu-rosen-astro-group namespace and available for use:

| PVC Name | Storage Class | Options | Data Description |
| -------- | ---- | ------- | ---------------- |
| shared | rook-cephfs-tide | ReadWriteMany | This PVC contains shared data for the entire group| 

## Example Code

- [Running MESA Batch Jobs](/mesa)
