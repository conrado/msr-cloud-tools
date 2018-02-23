MSR Cloud Tools
===============

Some Model Specific Register (MSR) tools for Xen guests (eg, AWS EC2).

## Prereqs

So far only written for Intel(R) Xeon(R) CPU E5-2670 v2s (Ivy Bridge).

Tested on Ubuntu Trusty.

```
# sudo apt-get install msr-tools
# sudo modprobe msr
```

## Contents

- [showboost](showboost): show the real CPU clock rate to understand the current level of turbo boost.
- [cputemp](cputemp): show per-CPU temperatures.
- [cpuhot](cpuhot): show per-CPU temperature throttle flags (from IA32_THERM_STATUS 15:0), for evidence of thermal throttling.

## Screenshots

Measure the actual clock rate for CPU 0:

<pre>
# <b>./showboost</b>
CPU MHz      : 2500
Turbo MHz    : 3100 3200 3300 3500
Turbo Ratios : 124% 128% 132% 140%
CPU 0 summary every 1 seconds...

TIME       C0_MCYC      C0_ACYC        UTIL  RATIO    MHz
23:24:59   968524994    1200782482      38%   123%   3099
23:25:00   975813066    1207391520      39%   123%   3093
23:25:01   951743868    1180005763      38%   123%   3099
23:25:02   954477820    1182323893      38%   123%   3096
23:25:03   956817093    1186429567      38%   123%   3099
[...]
</pre>

Show average CPU utilization, and per-CPU temperatures, every second:

<pre>
# <b>./cputemp -u 1</b>
AvgUtil CPU1 CPU2 CPU3 CPU4 CPU5 CPU6 CPU7 CPU8 CPU9 CPU10 CPU11 CPU12 CPU13 CPU14 CPU15 CPU16
56 77 77 77 73 76 78 77 72 77 76 76 74 75 79 77 73
57 77 76 77 75 75 79 76 72 77 76 77 74 76 78 77 73
57 77 76 77 74 76 78 76 73 77 77 77 73 76 78 77 72
57 77 76 77 73 76 78 77 73 77 76 77 74 76 79 77 73
57 77 77 77 73 76 78 77 72 77 76 77 74 76 78 75 72
57 77 77 77 73 76 79 76 73 77 76 77 73 76 79 76 73
58 77 76 77 73 76 78 77 72 77 77 77 74 77 78 77 73
[...]
</pre>

Check that no CPU thermal throttled flags have been set:

<pre>
# <b>./cpuhot</b>
- CPU1 CPU2 CPU3 CPU4 CPU5 CPU6 CPU7 CPU8 CPU9 CPU10 CPU11 CPU12 CPU13 CPU14 CPU15 CPU16
PROCHOT 95 95 95 95 95 95 95 95 95 95 95 95 95 95 95 95
Celsius 77 75 76 73 76 77 75 72 76 72 75 77 76 72 76 75
Flags 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0 0x0
</pre>
