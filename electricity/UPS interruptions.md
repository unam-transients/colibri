# UPS Interruptions

## American UPS

### 2026-01-21

I talked to Edgar. He confirmed that the UPS is configured to do a self-test at
00:00 local time = 08:00 UTC every second Tuesday. This explains these
interruptions.

He has configured the tests to be every fourth Tuesday at 11:00 local time =
19:00 UTC.

When we discussed this, Stéphane asked why we did not see this before September.
I only programmed reporting of the battery levels in September 2025. Before that
I just logged alarms. However, there were UPS alarms just after 08:00 UTC on:

> 2025-02-18, 2025-03-04, 2025-03-18, 2025-04-01, 2025-04-15, 2025-04-29,
> 2025-05-13, 2025-05-27, 2025-06-10, 2025-06-24, 2025-07-08, 2025-07-22,
> 2025-08-05, 2025-08-19, 2025-09-02, 2025-09-16, 2025-10-14, 2025-10-28,
> 2025-11-11, 2025-11-25, 2025-12-09, and 2025-12-23.

These are every two weeks.

### 2026-01-20

We have seen five problems with the American UPS in the last three months.
These happen *exactly* two weeks apart.
The pattern is the same:

- At about 08:10 UTC the UPS changes from line to battery
- At about 08:25 UTC it reaches 90% charge and closes the telescope
- At about 08:40 UTC it starts charging again
- At about 10:10 UTC it reaches 96% and the telescope can open again
- At about 11:20 UTC it reaches 100% charge

When this happens, we lose almost two hours of observation.

It's not clear to me why we discharge to 90% and then stop. The major loads on
the European UPS are the compressors, the computers, and the dome. Perhaps the
dome dominates the load?

The current algorithm for the UPS alarm is:

- set the alarm when the battery reaches 90%
- clear the alarm when the battery recharges to 96%

I would propose changing this to:

- set the alarm when the battery reaches 90%
- clear the alarm when the battery recharges to 91%

This would reduce the closures from almost two hours to about 15 minutes in the
cases we have seen.

## European UPS

### 2026-01-22

Edgar programmed a self-test during the day. It showed exactly the same pattern
as the interruptions in the night, which confirms that these are self-tests.

The manual does not allow us to configure the times of these self tests. They
automatically occur every 24 hours after the UPS is initialized. Edgar turned
the UPS off and on at 12:00 PDT (20:00 UTC) in order that the self-tests occur
during the day.

### 2026-01-20

Almost every night at 08:00 UTC, the European UPS switches to battery,
discharges to 98% in about 20 seconds, and then charges back to 100% over the
course of the next half hour.

This seems to happen whether the telescope is open or not.

## Appendix: Discharge Events for the American UPS

```text
2025-11-11 08:10:01.957 plcserver: summary: american ups battery charge level has changed from 100% to 99%.
2025-11-11 08:25:43.828 plcserver: summary: american ups battery charge level has changed from 91% to 90%.
2025-11-11 08:36:42.209 plcserver: summary: american ups battery charge level has changed from 90% to 91%.
2025-11-11 10:06:43.378 plcserver: summary: american ups battery charge level has changed from 95% to 96%.
2025-11-11 11:18:44.232 plcserver: summary: american ups battery charge level has changed from 99% to 100%.

2025-11-25 08:10:31.717 plcserver: summary: american ups battery charge level has changed from 100% to 99%.
2025-11-25 08:26:39.871 plcserver: summary: american ups battery charge level has changed from 91% to 90%.
2025-11-25 08:45:38.575 plcserver: summary: american ups battery charge level has changed from 90% to 91%.
2025-11-25 10:15:38.575 plcserver: summary: american ups battery charge level has changed from 95% to 96%.
2025-11-25 11:27:37.953 plcserver: summary: american ups battery charge level has changed from 99% to 100%.

2025-12-09 08:09:54.700 plcserver: summary: american ups battery charge level has changed from 100% to 99%.
2025-12-09 08:27:18.848 plcserver: summary: american ups battery charge level has changed from 91% to 90%.
2025-12-09 08:43:30.367 plcserver: summary: american ups battery charge level has changed from 90% to 91%.
2025-12-09 10:13:31.161 plcserver: summary: american ups battery charge level has changed from 95% to 96%.
2025-12-09 11:25:30.265 plcserver: summary: american ups battery charge level has changed from 99% to 100%.

2025-12-23 08:10:20.982 plcserver: summary: american ups battery charge level has changed from 100% to 99%.
2025-12-23 08:25:47.302 plcserver: summary: american ups battery charge level has changed from 91% to 90%.
2025-12-23 08:41:06.115 plcserver: summary: american ups battery charge level has changed from 90% to 91%.
2025-12-23 10:11:06.391 plcserver: summary: american ups battery charge level has changed from 95% to 96%.
2025-12-23 11:23:05.266 plcserver: summary: american ups battery charge level has changed from 99% to 100%.

2026-01-06 08:10:34.095 plcserver: summary: american ups battery charge level has changed from 100% to 99%.
2026-01-06 08:26:53.266 plcserver: summary: american ups battery charge level has changed from 91% to 90%.
2026-01-06 08:40:25.480 plcserver: summary: american ups battery charge level has changed from 90% to 91%.
2026-01-06 10:10:27.052 plcserver: summary: american ups battery charge level has changed from 95% to 96%.
2026-01-06 11:22:26.993 plcserver: summary: american ups battery charge level has changed from 99% to 100%.

2026-01-20 08:10:58.831 plcserver: summary: american ups battery charge level has changed from 100% to 99%.
2026-01-20 08:28:08.627 plcserver: summary: american ups battery charge level has changed from 91% to 90%.
2026-01-20 08:40:38.019 plcserver: summary: american ups battery charge level has changed from 90% to 91%.
2026-01-20 10:10:38.565 plcserver: summary: american ups battery charge level has changed from 95% to 96%.
2026-01-20 11:22:38.335 plcserver: summary: american ups battery charge level has changed from 99% to 100%.
```

## Appendix: Discharge Events for the European UPS

```text
2025-10-29 08:00:11.930 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-10-29 08:00:17.128 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-10-29 08:02:03.273 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-10-29 08:29:03.740 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-10-30 08:00:12.940 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-10-30 08:00:19.256 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-10-30 08:01:56.703 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-10-30 08:28:51.832 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-10-31 08:00:13.532 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-10-31 08:00:19.289 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-10-31 08:01:59.121 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-10-31 08:29:00.279 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-04 08:00:12.601 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-04 08:00:19.482 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-04 08:01:44.094 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-04 08:28:39.078 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-05 08:00:13.351 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-05 08:00:19.671 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-05 08:01:36.841 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-05 08:28:16.690 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-06 08:00:13.664 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-06 08:00:20.582 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-06 08:02:00.151 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-06 08:28:54.335 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-07 08:00:11.953 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-07 08:00:19.476 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-07 08:01:47.124 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-07 08:28:45.549 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-08 08:00:12.092 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-08 08:00:20.167 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-08 08:01:47.799 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-08 08:28:42.444 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-09 08:00:15.410 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-09 08:00:21.769 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-09 08:01:53.299 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-09 08:28:53.562 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-10 08:00:12.105 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-10 08:00:19.625 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-10 08:01:54.752 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-10 08:28:49.996 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-11 08:00:12.177 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-11 08:00:18.529 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-11 08:01:54.782 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-11 08:28:52.723 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-12 08:00:13.865 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-12 08:00:19.062 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-12 08:01:41.437 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-12 08:28:41.736 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-13 08:00:12.203 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-13 08:00:17.407 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-13 08:01:31.822 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-13 08:28:29.946 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-14 08:00:13.239 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-14 08:00:18.993 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-14 08:01:13.134 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-14 08:27:56.085 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-15 08:00:14.275 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-15 08:00:20.595 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-15 08:01:12.493 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-15 08:27:48.286 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-16 08:00:11.723 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-16 08:00:18.641 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-16 08:01:03.023 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-16 08:27:38.532 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-17 08:00:13.150 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-17 08:00:19.506 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-17 08:01:06.848 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-17 08:27:55.137 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-18 08:00:13.148 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-18 08:00:20.062 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-18 08:01:07.286 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-18 08:27:53.653 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-19 08:00:14.447 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-19 08:00:20.206 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-19 08:01:10.345 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-19 08:28:03.167 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-20 08:00:13.006 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-20 08:00:19.880 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-20 08:01:09.003 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-20 08:28:02.345 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-21 08:00:13.259 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-21 08:00:20.180 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-21 08:01:08.565 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-21 08:27:57.503 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-22 08:00:14.174 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-22 08:00:20.493 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-22 08:01:06.638 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-22 08:27:52.559 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-23 08:00:15.049 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-23 08:00:21.410 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-23 08:01:09.230 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-23 08:27:55.177 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-24 08:00:13.421 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-24 08:00:19.186 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-24 08:01:07.006 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-24 08:27:55.226 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-25 08:00:14.561 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-25 08:00:20.917 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-25 08:01:12.220 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-25 08:28:08.084 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-26 08:00:13.871 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-26 08:00:19.630 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-26 08:02:09.233 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-26 08:29:09.756 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-27 08:00:12.015 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-27 08:00:17.773 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-27 08:01:42.424 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-27 08:28:42.105 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-28 08:00:12.921 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-28 08:00:18.677 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-28 08:01:48.009 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-28 08:28:48.069 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-29 08:00:13.342 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-29 08:00:19.114 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-29 08:01:44.023 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-29 08:28:44.578 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-11-30 08:00:11.960 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-11-30 08:00:18.888 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-11-30 08:01:45.559 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-11-30 08:28:44.196 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-01 08:00:12.108 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-01 08:00:18.443 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-01 08:02:00.539 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-01 08:29:00.801 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-02 08:00:13.871 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-02 08:00:19.082 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-02 08:01:12.696 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-02 08:28:00.753 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-03 08:00:14.822 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-03 08:00:20.035 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-03 08:01:06.799 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-03 08:27:48.444 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-04 08:00:12.061 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-04 08:00:19.000 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-04 08:01:06.321 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-04 08:27:51.730 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-05 08:00:14.743 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-05 08:00:20.516 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-05 08:01:57.700 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-05 08:28:59.157 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-06 08:00:14.516 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-06 08:00:20.891 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-06 08:01:54.976 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-06 08:28:55.131 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-07 08:00:12.766 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-07 08:00:20.263 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-07 08:01:43.930 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-07 08:28:28.078 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-08 08:00:15.391 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-08 08:00:19.437 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-08 08:01:42.546 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-08 08:28:39.868 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-09 08:00:15.226 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-09 08:00:20.434 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-09 08:01:41.855 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-09 08:28:40.970 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-10 08:00:14.377 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-10 08:00:20.147 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-10 08:01:49.026 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-10 08:28:48.940 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-11 08:00:12.059 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-11 08:00:18.993 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-11 08:01:48.648 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-11 08:28:38.460 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-12 08:00:13.525 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-12 08:00:18.733 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-12 08:01:59.667 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-12 08:28:56.890 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-13 08:00:13.206 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-13 08:00:20.140 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-13 08:01:10.345 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-13 08:27:57.842 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-14 08:00:13.127 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-14 08:00:20.022 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-14 08:01:47.213 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-14 08:28:46.535 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-15 08:00:13.039 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-15 08:00:18.851 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-15 08:01:48.970 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-15 08:28:49.367 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-16 08:00:13.243 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-16 08:00:19.572 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-16 08:01:57.789 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-16 08:28:57.864 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-17 08:00:13.654 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-17 08:00:18.263 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-17 08:01:48.417 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-17 08:28:47.036 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-18 08:00:14.154 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-18 08:00:20.486 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-18 08:02:07.470 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-18 08:29:07.394 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-19 08:00:13.437 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-19 08:00:20.332 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-19 08:01:44.677 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-19 08:28:43.947 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-20 08:00:11.035 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-20 08:00:18.562 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-20 08:01:34.776 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-20 08:28:32.960 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-21 08:00:14.901 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-21 08:00:18.950 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-21 08:01:51.953 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-21 08:28:47.213 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-22 08:00:14.805 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-22 08:00:21.176 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-22 08:01:51.779 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-22 08:28:51.858 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-23 08:00:13.177 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-23 08:00:20.111 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-23 08:01:43.815 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-23 08:28:24.736 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-24 08:00:14.311 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-24 08:00:20.082 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-24 08:01:09.726 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-24 08:27:50.953 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-25 08:00:15.463 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-25 08:00:20.673 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-25 08:01:09.801 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-25 08:27:49.845 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-26 08:00:16.035 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-26 08:00:20.638 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-26 08:01:10.289 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-26 08:27:49.171 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-27 08:00:11.647 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-27 08:00:18.013 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-27 08:01:58.174 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-27 08:28:57.391 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-28 08:00:12.674 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-28 08:00:19.604 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-28 08:01:52.687 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-28 08:28:52.989 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-29 08:00:13.864 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-29 08:00:19.631 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-29 08:02:01.848 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-29 08:29:02.288 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-30 08:00:12.509 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-30 08:00:18.269 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-30 08:01:07.851 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-30 08:27:51.756 plcserver: summary: european ups battery level has changed from 99% to 100%.

2025-12-31 08:00:13.308 plcserver: summary: european ups battery level has changed from 100% to 99%.
2025-12-31 08:00:18.506 plcserver: summary: european ups battery level has changed from 99% to 98%.
2025-12-31 08:01:49.036 plcserver: summary: european ups battery level has changed from 98% to 99%.
2025-12-31 08:28:49.295 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-01 08:00:14.013 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-01 08:00:20.371 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-01 08:01:12.236 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-01 08:27:53.582 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-02 08:00:12.128 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-02 08:00:19.042 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-02 08:01:09.111 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-02 08:27:48.298 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-03 08:00:13.328 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-03 08:00:20.246 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-03 08:01:57.575 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-03 08:28:53.960 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-04 08:00:11.667 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-04 08:00:16.868 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-04 08:01:10.970 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-04 08:27:57.868 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-05 08:00:14.163 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-05 08:00:21.638 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-05 08:01:46.933 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-05 08:28:47.207 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-06 08:00:13.263 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-06 08:00:19.019 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-06 08:02:04.907 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-06 08:29:04.503 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-07 08:00:14.098 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-07 08:00:19.858 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-07 08:01:42.190 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-07 08:28:39.989 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-08 08:00:15.009 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-08 08:00:20.805 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-08 08:02:03.335 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-08 08:29:01.348 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-09 08:00:12.792 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-09 08:00:19.153 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-09 08:01:46.842 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-09 08:28:45.223 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-10 08:00:15.088 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-10 08:00:20.845 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-10 08:01:50.694 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-10 08:28:49.911 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-11 08:00:12.292 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-11 08:00:18.653 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-11 08:01:51.979 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-11 08:28:50.516 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-12 08:00:13.736 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-12 08:00:19.493 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-12 08:01:55.960 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-12 08:28:55.920 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-13 08:00:12.436 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-13 08:00:18.233 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-13 08:01:58.437 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-13 08:28:58.161 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-14 08:00:13.005 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-14 08:00:18.759 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-14 08:01:59.005 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-14 08:28:56.226 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-15 08:00:13.819 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-15 08:00:19.575 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-15 08:01:47.746 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-15 08:28:45.887 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-16 08:00:12.019 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-16 08:00:18.377 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-16 08:01:46.506 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-16 08:28:46.654 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-17 08:00:13.759 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-17 08:00:19.522 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-17 08:01:43.651 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-17 08:28:41.904 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-18 08:00:14.368 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-18 08:00:20.125 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-18 08:01:40.217 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-18 08:28:39.739 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-19 08:00:12.766 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-19 08:00:20.279 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-19 08:01:59.506 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-19 08:28:57.766 plcserver: summary: european ups battery level has changed from 99% to 100%.

2026-01-20 08:00:12.808 plcserver: summary: european ups battery level has changed from 100% to 99%.
2026-01-20 08:00:19.125 plcserver: summary: european ups battery level has changed from 99% to 98%.
2026-01-20 08:01:53.410 plcserver: summary: european ups battery level has changed from 98% to 99%.
2026-01-20 08:28:51.992 plcserver: summary: european ups battery level has changed from 99% to 100%.
```
