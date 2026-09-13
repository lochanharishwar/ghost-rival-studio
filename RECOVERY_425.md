# Recovery of the 425-frame stall

The previous server process exited at approximately 10:14:37 on September 13, immediately after this analysis stopped writing results. Its SQLite status remained running. The replacement server did not own the job.

Partial files and the original job record are preserved under data/recovery/2ebaf609ab7f48e2b3872ea32183cf3f. The same job was marked interrupted and restarted through the API. Restart reconstructs tracking from the beginning; it does not claim to resume missing tracking state at frame 426.

New jobs record process ID and process creation time. The state API reconciles jobs whose worker has exited or whose PID was reused, marking them interrupted instead of leaving a permanent running status. Live workers are preserved. Two regression tests cover live and dead workers; the full suite passes 28 tests.
