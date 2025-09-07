---
description: Documentation of the IPC (Inter-Process Communication) API.
icon: satellite-dish
---

# Inter-Process Communication

IPC allows processes to communicate and share variables with other processes, which the standard sandbox does not allow them to do.

The IPC library does not need to be `require`d. It is in the public runtime environment by default.

* `ipc.shareWithAll(): table`\
  Returns a share table. All data in the table is accessible (though read-only) to all other processes.
* `ipc.shareWith(pid: number): table`\
  Returns a share table. All data in the table is accessible (though read-only) to the process with the PID specified.
* `ipc.shared: table`\
  This contains the tables (keyed by PIDs) of processes sharing variables with the current process over IPC. This table should only be indexed.
  * `ipc.shared[pid: number]: table`\
    This contains all variables (if any) shared with the current process from the process with a PID of `pid`.
