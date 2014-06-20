The asm_metrics.pl utility is used to display ASM real-time metrics. It basically takes a snapshot each second (default interval) from the gv$asm_disk_iostat (or gv$asm_disk_stat depending of the version) cumulative view and computes the delta with the previous snapshot.

This utility:

- provides useful metrics.
- is RAC aware.
- is fully customizable: you can aggregate the results depending on your needs.
- does not install anything into the database or ASM instance.

It displays the following metrics:

- Reads/s: Number of read per second.
- KbyRead/s: Kbytes read per second.
- Avg ms/Read: ms per read in average.
- AvgBy/Read: Average Bytes per read.
- Same metrics are provided for Write Operations.

At the following levels:

- ASM Instance.
- Database Instance.
- ASM Diskgroup.
- ASM Failgroup (Or cell’s IP on Exadata).
- Disks.
