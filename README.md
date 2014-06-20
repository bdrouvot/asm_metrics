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

Let’s see the help:

./asm_metrics.pl -help

Usage: ./asm_metrics.pl [-interval] [-count] [-inst] [-dbinst] [-dg] [-fg] [-ip] [-show] [-display] [-sort_field] [-help]

Default Interval : 1 second.
Default Count    : Unlimited

Parameter         Comment                                                           Default
---------         -------                                                           -------
-INST=            ALL - Show all Instance(s)                                        ALL
                  CURRENT - Show Current Instance
                  INSTANCE_NAME,... - choose Instance(s) to display

-DBINST=          Database Instance to collect (Wildcard allowed)                   ALL
-DG=              Diskgroup to collect (Wildcard allowed)                           ALL
-FG=              Failgroup to collect (Wildcard allowed)                           ALL
-IP=              IP (Exadata Cells) to collect (Wildcard allowed)                  ALL
-SHOW=            What to show: inst,dbinst,fg|ip,dg,dsk (comma separated list)     DG
-DISPLAY=         What to display: snap,avg (comma separated list)                  SNAP
-SORT_FIELD=      reads|writes|iops                                                 NONE

- Example: ./asm_metrics.pl
- Example: ./asm_metrics.pl  -inst=+ASM1
- Example: ./asm_metrics.pl  -dg=DATA -show=dg
- Example: ./asm_metrics.pl  -dg=data -show=inst,dg,fg
- Example: ./asm_metrics.pl  -show=dg,dsk
- Example: ./asm_metrics.pl  -show=inst,dg,fg,dsk
- Example: ./asm_metrics.pl  -interval=5 -count=3 -sort_field=iops
- Example: ./asm_metrics.pl  -show=dg -display=avg -sort_field=iops
- Example: ./asm_metrics.pl  -show=dg -display=snap,avg -sort_field=iops

The main options/features are:

- You can choose the number of snapshots to display and the time to wait between snapshots.
- You can choose on which ASM instance to collect the metrics thanks to the -INST= parameter.
- You can choose for which DB instance to collect the metrics thanks to the -DBINST= parameter (wildcard allowed).
- You can choose on which Diskgroup to collect the metrics thanks to the -DG= parameter (wildcard allowed).
- You can choose on which Failgroup to collect the metrics thanks to the -FG= parameter (wildcard allowed).
- You can choose on which Exadata Cells to collect the metrics thanks to the -IP= parameter (wildcard allowed).
- You can aggregate the results on the ASM instances, DB instances, Diskgroup, Failgroup (or Exadata cells IP) level thanks to the -SHOW= parameter.
- You can display the metrics per snapshot, the average metrics value since the collection began (that is to say since the script has been launched) or both thanks to the -DISPLAY= parameter.
- You can sort based on the number of reads, number of writes or number of IOPS (reads+writes) thanks to the -SORT_FIELD= parameter
