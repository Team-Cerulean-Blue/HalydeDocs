---
description: Documentation of the Halyde kernel's task scheduler.
icon: calendar-pen
---

# Task Scheduler

## Under the hood

Halyde supports multitasking by using coroutines, a feature included in Lua 5.0 and later. Coroutines work differently than threads: when a coroutine gets ran, the code that runs the coroutine gets paused, and the coroutine will run until it runs `coroutine.yield()`, which will resume the main code afterwards

The task scheduler (`/halyde/kernel/tsched.lua`) uses these coroutines to simulate multitasking, by storing the coroutines onto a table, and running them one-by-one everytime. This means that the process code will continue executing until it runs `coroutine.yield()`.

OpenComputers (specifically `machine.lua`) imposes that every coroutine must run `coroutine.yield()` with an interval of 10 or less seconds, otherwise it will yield the error `too long without yielding`. This applies to all processes (from the kernel, from an user-installed driver, the shell, or an app).

## Public space API

This is for interacting with the task scheduler, for getting, creating, and killing tasks. If the code is a kernel module, the task scheduler is available in `_PUBLIC.tsched`, otherwise in `tsched`.

* `tsched.addTask(func: function, name: string)` \
  Creates a task from a function. This function will run with the environment that it has been created in: these tasks created by the kernel will run in the kernel environment, but tasks created by the shell or an app will run with their user environment.
* `tsched.runAsTask(path: string, ...)` \
  Creates a task from an executable file in a certain path, with arguments to pass through. The environment of all processes created through this function is confined in their own copy of the public space (stored as `_PUBLIC` in the kernel). If any process adds anything to its environment, it will not be visible to other processes unless it allows communication through [IPC](../libraries-and-apis/inter-process-communication.md).
* `tsched.removeTask(id: number): boolean` \
  Removes a task based from a process ID. Returns `true` if successful, otherwise `false`.
* `tsched.getCurrentTask(): table` \
  Returns the current task that is being ran. If this is called from a process, returns table of said process. The table that gets returned contains `task`, `name`, and `id` for the Lua coroutine, process name, and process id respectively.
* `tsched.getTasks(): table` \
  Returns all the tasks in a list, where every task is in the same format as the table returned by `tsched.getCurrentTask`.
