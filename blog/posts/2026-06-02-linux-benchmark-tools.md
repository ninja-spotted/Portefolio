---
title:  "Linux benchmark tools"
parent: Blog
permalink: "/blog/linux-benchmark-tools"
layout: default
date:   2026-06-03
last_modified_date: 2026-06-03
---

# Linux benchmark tools

For a while now, I have been wondering how to compare the performance of the many linux devices I have come across in my life.

I am a big fan of benchmarks and used to watch YT videos from channels like HardwareUnboxed and RandomGaminginHD for their interesting
benchmarks while testing computer hardware. In those, they mostly compared using built in applications for benchmark or certain games.

## What exists nowadays for benchmarking linux systems?

For linux, I think there are less comercial products for benchmarking, but there are a lot of other options:

- [Jeff Geerling SBC reviews](https://github.com/geerlingguy/sbc-reviews)

- [Phoronix Test Suite](https://github.com/phoronix-test-suite/phoronix-test-suite/releases/)

- [Blender Benchmark](https://opendata.blender.org/)



### Other options

There are many, many other programs that include or exist to collect data about the performance of a system. Some of them can be found in [Archlinux Wiki](https://wiki.archlinux.org/title/Benchmarking).

#### fio (Disk benchmark)

`sudo apt install fio`

Run `fio` with:

    sudo fio --filename=/mnt/test.fio --size=8GB --direct=1 --rw=randrw --bs=4k --ioengine=libaio --iodepth=256 --runtime=120 --numjobs=4 --time_based --group_reporting --name=iops-test-job --eta-newline=1

After a few minutes, the result is output to the terminal:

    iops-test-job: (groupid=0, jobs=4): err= 0: pid=12811: Tue Jun  2 22:48:41 2026
    read: IOPS=56.8k, BW=222MiB/s (233MB/s)(26.0GiB/120005msec)
        slat (usec): min=4, max=193532, avg= 7.21, stdev=169.31
        clat (usec): min=462, max=668187, avg=8526.47, stdev=27648.39
        lat (usec): min=472, max=668196, avg=8533.67, stdev=27649.75
        clat percentiles (usec):
        |  1.00th=[  1385],  5.00th=[  2024], 10.00th=[  2540], 20.00th=[  3425],
        | 30.00th=[  3851], 40.00th=[  4113], 50.00th=[  4490], 60.00th=[  4883],
        | 70.00th=[  5342], 80.00th=[  6128], 90.00th=[  7832], 95.00th=[ 11731],
        | 99.00th=[133694], 99.50th=[210764], 99.90th=[341836], 99.95th=[404751],
        | 99.99th=[488637]
    bw (  KiB/s): min= 4661, max=449584, per=100.00%, avg=227397.40, stdev=41083.95, samples=956
    iops        : min= 1165, max=112396, avg=56849.20, stdev=10271.03, samples=956
    write: IOPS=56.8k, BW=222MiB/s (233MB/s)(26.0GiB/120005msec); 0 zone resets
        slat (usec): min=5, max=193496, avg= 7.74, stdev=173.75
        clat (usec): min=1027, max=668734, avg=9487.19, stdev=29832.94
        lat (usec): min=1032, max=668743, avg=9494.93, stdev=29834.50
        clat percentiles (usec):
        |  1.00th=[  1958],  5.00th=[  2606], 10.00th=[  3097], 20.00th=[  3949],
        | 30.00th=[  4359], 40.00th=[  4621], 50.00th=[  5014], 60.00th=[  5407],
        | 70.00th=[  5932], 80.00th=[  6783], 90.00th=[  8586], 95.00th=[ 12649],
        | 99.00th=[185598], 99.50th=[291505], 99.90th=[396362], 99.95th=[413139],
        | 99.99th=[505414]
    bw (  KiB/s): min= 4458, max=446624, per=100.00%, avg=227231.99, stdev=41044.99, samples=956
    iops        : min= 1114, max=111656, avg=56807.82, stdev=10261.29, samples=956
    lat (usec)   : 500=0.01%, 750=0.01%, 1000=0.05%
    lat (msec)   : 2=2.88%, 4=25.16%, 10=64.87%, 20=3.85%, 50=1.06%
    lat (msec)   : 100=0.56%, 250=1.08%, 500=0.48%, 750=0.01%
    cpu          : usr=4.87%, sys=22.71%, ctx=881312, majf=0, minf=58
    IO depths    : 1=0.1%, 2=0.1%, 4=0.1%, 8=0.1%, 16=0.1%, 32=0.1%, >=64=100.0%
        submit    : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.0%
        complete  : 0=0.0%, 4=100.0%, 8=0.0%, 16=0.0%, 32=0.0%, 64=0.0%, >=64=0.1%
        issued rwts: total=6817922,6813261,0,0 short=0,0,0,0 dropped=0,0,0,0
        latency   : target=0, window=0, percentile=100.00%, depth=256

    Run status group 0 (all jobs):
    READ: bw=222MiB/s (233MB/s), 222MiB/s-222MiB/s (233MB/s-233MB/s), io=26.0GiB (27.9GB), run=120005-120005msec
    WRITE: bw=222MiB/s (233MB/s), 222MiB/s-222MiB/s (233MB/s-233MB/s), io=26.0GiB (27.9GB), run=120005-120005msec

    Disk stats (read/write):
    nvme0n1: ios=6813017/6808536, sectors=54504160/54473512, merge=0/217, ticks=57156641/62842927, in_queue=120001754, util=76.88%


#### 7z benchmark (Compressing and decompressing tasks)

To run this benchmark, just run `7z b`:

    7-Zip 23.01 (x64) : Copyright (c) 1999-2023 Igor Pavlov : 2023-06-20
    64-bit locale=en_US.UTF-8 Threads:16 OPEN_MAX:1024

    Compiler: 13.2.0 GCC 13.2.0: SSE2
    Linux : 6.8.0-117-generic : #117-Ubuntu SMP PREEMPT_DYNAMIC Tue May  5 19:26:24 UTC 2026 : x86_64
    PageSize:4KB THP:madvise hwcap:2 hwcap2:2
    AMD Ryzen 7 7735HS with Radeon Graphics (A40F41) 

    1T CPU Freq (MHz):  1355  1354  1354  1353  1620  2378  2378
    8T CPU Freq (MHz): 734% 2134   773% 2248  

    RAM size:   15226 MB,  # CPU hardware threads:  16
    RAM usage:   3559 MB,  # Benchmark threads:     16

                        Compressing  |                  Decompressing
    Dict     Speed Usage    R/U Rating  |      Speed Usage    R/U Rating
            KiB/s     %   MIPS   MIPS  |      KiB/s     %   MIPS   MIPS

    22:      32930  1180   2715  32035  |     542792  1440   3215  46284
    23:      56028  1345   4243  57086  |     679485  1443   4073  58780
    24:      53996  1374   4226  58057  |     675271  1477   4012  59250
    25:      50740  1353   4282  57934  |     650063  1464   3949  57837
    ----------------------------------  | ------------------------------
    Avr:     48423  1313   3866  51278  |     636903  1456   3812  55538
    Tot:            1385   3839  53408

