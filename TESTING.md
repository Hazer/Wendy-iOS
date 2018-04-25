# Test the following scenarios:

* Call PendingTasks.runAllTasks() 2+ times immediately next to each other and assert that (1) both calls to PendingTasks.runAllTasks() returns instantly (testing the scheuling of those calls are async) and (2) the task runner runs through all pending tasks once and then starts all over again (showing that the task runner runs in a synchonized way and the 2+ calls to run all tasks do not interweave. They should wait their turn to run.)

* Call PendingTasks.runPendingTask(taskId) a couple of times, call PendingTasks.runAllTasks(), then again call PendingTasks.runPendingTask(taskId) to make sure that *all* 4 of those calls all run tasks in a synchonized way. None of them interweave each other and they all wait in line to run a single task. All you need to look for is that the call to PendingTasks.runAllTasks() does not jump in line and immediately begin running it's tasks. It needs to wait in line for the first 2 calls to PendingTasks.runPendingTask(taskId) to be done first.

* Create a PendingTask of tag FooPendingTask (or whatever) with dataId of 1, groupId null (doesn't matter). Run the task, while it is running, try to add the same type of PendingTask (the tag and dataId and groupId is the same) to Wendy. If the currently running task runs successful (if it fails, you have to simply try doing this test again) You should see in the logs Wendy saying that the task is *not* being deleted and is being re-run. The createdAt date should be updated on the existing PendingTask in Wendy, but not deleted (so the taskId is the same). 