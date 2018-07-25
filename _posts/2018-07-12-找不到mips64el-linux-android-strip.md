---
title: 找不到mips64el-linux-android-strip
date:  2018-07-12 15:03:30
categories:
- Android
tags:
- Android
- ndk
---
#### 完整的错误log:  

```java
org.gradle.api.tasks.TaskExecutionException: Execution failed for task ':app:transformNativeLibsWithStripDebugSymbolForCommonDebug'.
at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.executeActions(ExecuteActionsTaskExecuter.java:84)
at org.gradle.api.internal.tasks.execution.ExecuteActionsTaskExecuter.execute(ExecuteActionsTaskExecuter.java:55)
at org.gradle.api.internal.tasks.execution.SkipUpToDateTaskExecuter.execute(SkipUpToDateTaskExecuter.java:62)
at org.gradle.api.internal.tasks.execution.ValidatingTaskExecuter.execute(ValidatingTaskExecuter.java:58)
at org.gradle.api.internal.tasks.execution.SkipEmptySourceFilesTaskExecuter.execute(SkipEmptySourceFilesTaskExecuter.java:88)
at org.gradle.api.internal.tasks.execution.ResolveTaskArtifactStateTaskExecuter.execute(ResolveTaskArtifactStateTaskExecuter.java:46)
at org.gradle.api.internal.tasks.execution.SkipTaskWithNoActionsExecuter.execute(SkipTaskWithNoActionsExecuter.java:51)
at org.gradle.api.internal.tasks.execution.SkipOnlyIfTaskExecuter.execute(SkipOnlyIfTaskExecuter.java:54)
at org.gradle.api.internal.tasks.execution.ExecuteAtMostOnceTaskExecuter.execute(ExecuteAtMostOnceTaskExecuter.java:43)
at org.gradle.api.internal.tasks.execution.CatchExceptionTaskExecuter.execute(CatchExceptionTaskExecuter.java:34)
at org.gradle.execution.taskgraph.DefaultTaskGraphExecuter$EventFiringTaskWorker$1.execute(DefaultTaskGraphExecuter.java:236)
at org.gradle.execution.taskgraph.DefaultTaskGraphExecuter$EventFiringTaskWorker$1.execute(DefaultTaskGraphExecuter.java:228)
at org.gradle.internal.Transformers$4.transform(Transformers.java:169)
at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:106)
at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:61)
at org.gradle.execution.taskgraph.DefaultTaskGraphExecuter$EventFiringTaskWorker.execute(DefaultTaskGraphExecuter.java:228)
at org.gradle.execution.taskgraph.DefaultTaskGraphExecuter$EventFiringTaskWorker.execute(DefaultTaskGraphExecuter.java:215)
at org.gradle.execution.taskgraph.AbstractTaskPlanExecutor$TaskExecutorWorker.processTask(AbstractTaskPlanExecutor.java:77)
at org.gradle.execution.taskgraph.AbstractTaskPlanExecutor$TaskExecutorWorker.run(AbstractTaskPlanExecutor.java:58)
at org.gradle.execution.taskgraph.DefaultTaskPlanExecutor.process(DefaultTaskPlanExecutor.java:32)
at org.gradle.execution.taskgraph.DefaultTaskGraphExecuter.execute(DefaultTaskGraphExecuter.java:113)
at org.gradle.execution.SelectedTaskExecutionAction.execute(SelectedTaskExecutionAction.java:37)
at org.gradle.execution.DefaultBuildExecuter.execute(DefaultBuildExecuter.java:37)
at org.gradle.execution.DefaultBuildExecuter.access$000(DefaultBuildExecuter.java:23)
at org.gradle.execution.DefaultBuildExecuter$1.proceed(DefaultBuildExecuter.java:43)
at org.gradle.execution.DryRunBuildExecutionAction.execute(DryRunBuildExecutionAction.java:32)
at org.gradle.execution.DefaultBuildExecuter.execute(DefaultBuildExecuter.java:37)
at org.gradle.execution.DefaultBuildExecuter.execute(DefaultBuildExecuter.java:30)
at org.gradle.initialization.DefaultGradleLauncher$3.execute(DefaultGradleLauncher.java:196)
at org.gradle.initialization.DefaultGradleLauncher$3.execute(DefaultGradleLauncher.java:193)
at org.gradle.internal.Transformers$4.transform(Transformers.java:169)
at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:106)
at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:56)
at org.gradle.initialization.DefaultGradleLauncher.doBuildStages(DefaultGradleLauncher.java:193)
at org.gradle.initialization.DefaultGradleLauncher.doBuild(DefaultGradleLauncher.java:119)
at org.gradle.initialization.DefaultGradleLauncher.run(DefaultGradleLauncher.java:102)
at org.gradle.launcher.exec.GradleBuildController.run(GradleBuildController.java:71)
at org.gradle.tooling.internal.provider.runner.BuildModelActionRunner.run(BuildModelActionRunner.java:50)
at org.gradle.launcher.exec.ChainingBuildActionRunner.run(ChainingBuildActionRunner.java:35)
at org.gradle.tooling.internal.provider.runner.RunAsBuildOperationBuildActionRunner$1.execute(RunAsBuildOperationBuildActionRunner.java:43)
at org.gradle.tooling.internal.provider.runner.RunAsBuildOperationBuildActionRunner$1.execute(RunAsBuildOperationBuildActionRunner.java:40)
at org.gradle.internal.Transformers$4.transform(Transformers.java:169)
at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:106)
at org.gradle.internal.progress.DefaultBuildOperationExecutor.run(DefaultBuildOperationExecutor.java:56)
at org.gradle.tooling.internal.provider.runner.RunAsBuildOperationBuildActionRunner.run(RunAsBuildOperationBuildActionRunner.java:40)
at org.gradle.tooling.internal.provider.runner.SubscribableBuildActionRunner.run(SubscribableBuildActionRunner.java:75)
at org.gradle.launcher.exec.ChainingBuildActionRunner.run(ChainingBuildActionRunner.java:35)
at org.gradle.launcher.exec.InProcessBuildActionExecuter.execute(InProcessBuildActionExecuter.java:41)
at org.gradle.launcher.exec.InProcessBuildActionExecuter.execute(InProcessBuildActionExecuter.java:26)
at org.gradle.tooling.internal.provider.ContinuousBuildActionExecuter.execute(ContinuousBuildActionExecuter.java:75)
at org.gradle.tooling.internal.provider.ContinuousBuildActionExecuter.execute(ContinuousBuildActionExecuter.java:49)
at org.gradle.tooling.internal.provider.ServicesSetupBuildActionExecuter.execute(ServicesSetupBuildActionExecuter.java:44)
at org.gradle.tooling.internal.provider.ServicesSetupBuildActionExecuter.execute(ServicesSetupBuildActionExecuter.java:29)
at org.gradle.launcher.daemon.server.exec.ExecuteBuild.doBuild(ExecuteBuild.java:67)
at org.gradle.launcher.daemon.server.exec.BuildCommandOnly.execute(BuildCommandOnly.java:36)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.WatchForDisconnection.execute(WatchForDisconnection.java:47)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.ResetDeprecationLogger.execute(ResetDeprecationLogger.java:26)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.RequestStopIfSingleUsedDaemon.execute(RequestStopIfSingleUsedDaemon.java:34)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.ForwardClientInput$2.call(ForwardClientInput.java:74)
at org.gradle.launcher.daemon.server.exec.ForwardClientInput$2.call(ForwardClientInput.java:72)
at org.gradle.util.Swapper.swap(Swapper.java:38)
at org.gradle.launcher.daemon.server.exec.ForwardClientInput.execute(ForwardClientInput.java:72)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.LogAndCheckHealth.execute(LogAndCheckHealth.java:55)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.LogToClient.doBuild(LogToClient.java:60)
at org.gradle.launcher.daemon.server.exec.BuildCommandOnly.execute(BuildCommandOnly.java:36)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.EstablishBuildEnvironment.doBuild(EstablishBuildEnvironment.java:72)
at org.gradle.launcher.daemon.server.exec.BuildCommandOnly.execute(BuildCommandOnly.java:36)
at org.gradle.launcher.daemon.server.api.DaemonCommandExecution.proceed(DaemonCommandExecution.java:120)
at org.gradle.launcher.daemon.server.exec.StartBuildOrRespondWithBusy$1.run(StartBuildOrRespondWithBusy.java:50)
at org.gradle.launcher.daemon.server.DaemonStateCoordinator$1.run(DaemonStateCoordinator.java:297)
at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:54)
at org.gradle.internal.concurrent.StoppableExecutorImpl$1.run(StoppableExecutorImpl.java:40)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
at java.lang.Thread.run(Thread.java:745)
Caused by: org.gradle.process.internal.ExecException: A problem occurred starting process 'command '/Users/nicolite/Library/Android/sdk/ndk-bundle/toolchains/mips64el-linux-android-4.9/prebuilt/darwin-x86_64/bin/mips64el-linux-android-strip''
at org.gradle.process.internal.DefaultExecHandle.setEndStateInfo(DefaultExecHandle.java:198)
at org.gradle.process.internal.DefaultExecHandle.failed(DefaultExecHandle.java:329)
at org.gradle.process.internal.ExecHandleRunner.run(ExecHandleRunner.java:86)
... 5 more
Caused by: net.rubygrapefruit.platform.NativeException: Could not start '/Users/nicolite/Library/Android/sdk/ndk-bundle/toolchains/mips64el-linux-android-4.9/prebuilt/darwin-x86_64/bin/mips64el-linux-android-strip'
at net.rubygrapefruit.platform.internal.DefaultProcessLauncher.start(DefaultProcessLauncher.java:27)
at net.rubygrapefruit.platform.internal.WrapperProcessLauncher.start(WrapperProcessLauncher.java:36)
at org.gradle.process.internal.ExecHandleRunner.run(ExecHandleRunner.java:68)
... 5 more
Caused by: java.io.IOException: Cannot run program "/Users/nicolite/Library/Android/sdk/ndk-bundle/toolchains/mips64el-linux-android-4.9/prebuilt/darwin-x86_64/bin/mips64el-linux-android-strip" (in directory "/Users/nicolite/Git/android-nova/Nova"): error=2, No such file or directory
at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
at net.rubygrapefruit.platform.internal.DefaultProcessLauncher.start(DefaultProcessLauncher.java:25)
... 7 more
Caused by: java.io.IOException: error=2, No such file or directory
at java.lang.UNIXProcess.forkAndExec(Native Method)
at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
at java.lang.ProcessImpl.start(ProcessImpl.java:134)
at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
... 8 more
```

#### 解决方法  
如果ndk版本在r17版, 很有可能出现这个问题. 解决方案是:

先删除 Android/Sdk/ndk-bundle/ 下的内容

从 https://developer.android.google.cn/ndk/downloads/older_releases 下载16b版本的ndk到本地, 并解压说, 将解压缩后的所有文件拷贝到 Android/Sdk/ndk-bundle/ 目录下

重新build工程  

#### 参考
[Android Studio 报错显示 mips64el-linux-android-strip 找不到](https://blog.csdn.net/bylaven/article/details/80331345)  
