IDEA-317477
===========

Example project for [IDEA-317477](https://youtrack.jetbrains.com/issue/IDEA-317477).

This is a multi-module Gradle project with two submodules:

- test-java11 on language version 11
- test-java17 on language version 17

The project is opened from a WSL2 share (\\wsl$\Ubuntu\home\marcokrikke\git\test-jdk-idea) and the following JDKs are installed on WSL:

````
./gradlew -q javaToolchains

 + Options
     | Auto-detection:     Enabled
     | Auto-download:      Disabled

 + Azul Zulu JDK 1.8.0_372-b07
     | Location:           /usr/lib/jvm/zulu8-ca-amd64
     | Language Version:   8
     | Vendor:             Azul Zulu
     | Architecture:       amd64
     | Is JDK:             true
     | Detected by:        Common Linux Locations

 + Azul Zulu JDK 11.0.19+7-LTS
     | Location:           /usr/lib/jvm/zulu11-ca-amd64
     | Language Version:   11
     | Vendor:             Azul Zulu
     | Architecture:       amd64
     | Is JDK:             true
     | Detected by:        Common Linux Locations

 + Azul Zulu JDK 17.0.7+7-LTS
     | Location:           /usr/lib/jvm/zulu17-ca-amd64
     | Language Version:   17
     | Vendor:             Azul Zulu
     | Architecture:       amd64
     | Is JDK:             true
     | Detected by:        Current JVM
````

WSL info:

````
PS C:\Users\Marco.Krikke> C:\Windows\system32\wsl.exe --list --verbose
  NAME      STATE           VERSION
* Ubuntu    Running         2

PS C:\Users\Marco.Krikke> wsl -v
WSL version: 1.2.5.0
Kernel version: 5.15.90.1
WSLg version: 1.0.51
MSRDC version: 1.2.3770
Direct3D version: 1.608.2-61064218
DXCore version: 10.0.25131.1002-220531-1700.rs-onecore-base2-hyp
Windows version: 10.0.19045.2913
````

A Gradle reload gives the following output: `C:\usr\lib\jvm\zulu11-ca-amd64 doesn't exist`

No JDKs are installed on Windows.

Shell used on WSL: Fish (but issue also exists when switching to bash).

IntelliJ version information:

````
IntelliJ IDEA 2023.1.1 (Ultimate Edition)
Build #IU-231.8770.65, built on April 27, 2023
Licensed to ****
Subscription is active until ****
Runtime version: 17.0.6+10-b829.9 amd64
VM: OpenJDK 64-Bit Server VM by JetBrains s.r.o.
Windows 10.0
GC: G1 Young Generation, G1 Old Generation
Memory: 4096M
Cores: 16
Non-Bundled Plugins:
    net.sjrx.intellij.plugins.systemdunitfiles (223.230322.126)
    com.jetbrains.jax.ws (231.8109.90)
    com.intellij.gwt (231.8770.53)
    com.dmarcotte.handlebars (231.8770.3)
    org.sonarlint.idea (8.2.0.68615)

Kotlin: 231-1.8.21-IJ8770.65
````

Gradle version:

````
./gradlew --version

------------------------------------------------------------
Gradle 8.1.1
------------------------------------------------------------

Build time:   2023-04-21 12:31:26 UTC
Revision:     1cf537a851c635c364a4214885f8b9798051175b

Kotlin:       1.8.10
Groovy:       3.0.15
Ant:          Apache Ant(TM) version 1.10.11 compiled on July 10 2021
JVM:          17.0.7 (Azul Systems, Inc. 17.0.7+7-LTS)
OS:           Linux 5.15.90.1-microsoft-standard-WSL2 amd64
````

Relevant parts from IDEA log:

````
2023-05-09 09:05:44,451 [  13202]   INFO - #c.i.e.w.WslDistributionManager - Fetched WSL distributions: [(Ubuntu, version=2)] ("C:\Windows\system32\wsl.exe --list --verbose" done in 279 ms)
2023-05-09 09:05:44,635 [  13386]   INFO - #git4idea.commands.GitHandler - [.] git version
2023-05-09 09:05:44,996 [  13747]   INFO - #git4idea.commands.GitHandler - git version 2.40.1
2023-05-09 09:05:45,153 [  13904]   INFO - #c.i.o.e.u.ExternalSystemUtil - External project [//wsl$/Ubuntu/home/marcokrikke/git/test-jdk-idea] resolution task started
2023-05-09 09:05:45,214 [  13965]   INFO - #git4idea.config.GitExecutableManager - Git version for Ubuntu: /usr/bin/git: 2.40.1.0 (WSL2)
2023-05-09 09:05:45,216 [  13967]   INFO - #git4idea.commands.GitHandler - [.] git version
2023-05-09 09:05:45,419 [  14170]   INFO - #git4idea.commands.GitHandler - git version 2.40.1.windows.1
2023-05-09 09:05:45,433 [  14184]   INFO - #git4idea.config.GitExecutableManager - Git version for C:\Program Files\Git\cmd\git.exe: 2.40.1.0 (MSYS)
2023-05-09 09:05:45,482 [  14233]   INFO - #o.j.p.g.GradleManager - Instructing gradle to use java from \\wsl$\Ubuntu\usr\lib\jvm\zulu17-ca-amd64
2023-05-09 09:05:45,486 [  14237]   INFO - #o.j.k.i.script - [KOTLIN_SCRIPTING] Loading script definitions [org.gradle.kotlin.dsl.KotlinSettingsScript] using classpath: \\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-core-api-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-core-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-kotlin-dsl-tooling-models-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-kotlin-dsl-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\kotlin-stdlib-1.8.10.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\kotlin-compiler-embeddable-1.8.10.jar
2023-05-09 09:05:45,604 [  14355]   INFO - #o.j.p.g.GradleManager - Instructing gradle to use java from \\wsl$\Ubuntu\usr\lib\jvm\zulu17-ca-amd64
2023-05-09 09:05:45,607 [  14358]   INFO - #o.j.k.i.script - [KOTLIN_SCRIPTING] Loading script definitions [org.gradle.kotlin.dsl.KotlinBuildScript] using classpath: \\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-core-api-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-core-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-kotlin-dsl-tooling-models-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\gradle-kotlin-dsl-8.0.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\kotlin-stdlib-1.8.10.jar;\\wsl$\Ubuntu\home\marcokrikke\.gradle\wrapper\dists\gradle-8.0-bin\ca5e32bp14vu59qr306oxotwh\gradle-8.0\lib\kotlin-compiler-embeddable-1.8.10.jar
2023-05-09 09:05:45,861 [  14612]   INFO - #c.i.i.s.download - Selected pre-built shared index SharedIndexResult(request='JdkIndexRequest(sdkName=17, hash=null, aliases=[17.0.7, 17], kind=jdk)', url='https://index-cdn.jetbrains.com/v2/data/jdk/be297b39a5f05ccaa06ce6654534090de1ef8220/17.0.6-corretto-17.0.6-windows-1e3b19e6da7915e535ad5b92c52de5ead8d1d276c3c3be33013697047f441977.ijx.xz', weakHash=57e6205ab78d, sha256='1e3b19e6da7915e535ad5b92c52de5ead8d1d276c3c3be33013697047f441977') from https://index-cdn.jetbrains.com/v2/jdk/-17 for JdkIndexRequest(sdkName=17, hash=null, aliases=[17.0.7, 17], kind=jdk)
2023-05-09 09:05:45,864 [  14615]   INFO - #c.i.i.s.p.i.SharedIndexChunkConfigurationImpl - Shared index (17.0.6-corretto-17.0.6-1e3b19e6da7915e535ad5b92c52de5ead8d1d276c3c3be33013697047f441977-57e6205ab78d) already exists
2023-05-09 09:05:45,898 [  14649]   INFO - #c.i.e.wsl - WSL mount root for Ubuntu is /mnt/ (done in 430 ms)
2023-05-09 09:05:45,915 [  14666]   INFO - #c.i.i.s.p.i.SharedIndexChunkConfigurationImpl - Chunk 17.0.6-corretto-17.0.6-1e3b19e6da7915e535ad5b92c52de5ead8d1d276c3c3be33013697047f441977-57e6205ab78d is registered for project 'test-jdk-idea: matching: (fb=74, stub=141), incompatible: (fb=0, stub=0), unknown: (fb=9, stub=9), 
2023-05-09 09:05:45,965 [  14716]   INFO - #o.j.p.g.GradleManager - Instructing gradle to use java from \\wsl$\Ubuntu\usr\lib\jvm\zulu17-ca-amd64
2023-05-09 09:05:45,981 [  14732]   INFO - #o.j.p.g.GradleManager - Instructing gradle to use java from \\wsl$\Ubuntu\usr\lib\jvm\zulu17-ca-amd64
2023-05-09 09:05:46,112 [  14863]   INFO - #o.j.p.g.s.e.GradleExecutionHelper - Gradle system adjuster service: org.jetbrains.plugins.gradle.service.execution.GradleExecutionHelper$SystemPropertiesAdjuster
2023-05-09 09:05:48,904 [  17655]   INFO - #o.j.j.b.i.CompilerReferenceIndex - backward reference index version doesn't exist
2023-05-09 09:05:48,917 [  17668]   INFO - #c.i.c.b.IsUpToDateCheckStartupActivity - suitable consumer is not found
2023-05-09 09:05:48,924 [  17675]   INFO - c.i.s.k.s.d.SpaceKtsFileDetector - SpaceKtsFileDetector
2023-05-09 09:05:48,937 [  17688]   INFO - #c.j.r.p.c.CodeWithMeCleanup - running activity to cleanup old thin clients... Root path is 'C:\Users\Marco.Krikke\AppData\Local\JetBrains'. JvmStartTimeMs=1683615930830
2023-05-09 09:05:48,939 [  17690]   INFO - #c.j.r.p.c.CodeWithMeCleanup - found 0 Code With Me client system folders to check
2023-05-09 09:05:48,940 [  17691]   INFO - #c.j.r.p.c.CodeWithMeCleanup - found 1 Code With Me client config folders to check
2023-05-09 09:05:48,942 [  17693]   INFO - #c.j.r.p.c.CodeWithMeCleanup - keep only [223] major versions
2023-05-09 09:05:48,945 [  17696]   INFO - #c.i.d.WindowsDefenderCheckerActivity - real-time protection: false
2023-05-09 09:05:48,948 [  17699]   INFO - #c.j.r.p.c.CodeWithMeCleanup - keep config folder with version 223.7571.182, it is the most up-to-date config folder with 223 major version, path is 'C:\Users\Marco.Krikke\AppData\Roaming\JetBrains\JetBrainsClient223.7571.182'
2023-05-09 09:05:48,951 [  17702]   INFO - #c.i.r.OsRegistryConfigProvider - Looking for 'versionManagementEnabled' value in [HKLM_64\SOFTWARE\JetBrains\JetBrainsClient\versionManagementEnabled, HKLM_32\SOFTWARE\JetBrains\JetBrainsClient\versionManagementEnabled, HKCU_64\SOFTWARE\JetBrains\JetBrainsClient\versionManagementEnabled, HKCU_32\SOFTWARE\JetBrains\JetBrainsClient\versionManagementEnabled]
2023-05-09 09:05:48,952 [  17703]   INFO - #c.i.r.OsRegistryConfigProvider - OS provided value for 'versionManagementEnabled' is not found
2023-05-09 09:05:48,992 [  17743]   INFO - #c.i.w.i.i.GlobalWorkspaceModel - Sync global entities with mutable entity storage
2023-05-09 09:05:49,040 [  17791]   INFO - #c.i.w.i.i.EntitiesOrphanageImpl - Update orphanage. null modules added
2023-05-09 09:05:49,041 [  17792]   INFO - #c.i.w.i.i.WorkspaceModelImpl - Project model updated to version 5 in 19 ms: Apply JPS storage (iml files)
2023-05-09 09:05:49,041 [  17792]   INFO - #c.i.w.i.i.EntitiesOrphanageImpl - Update orphanage. null modules added
2023-05-09 09:05:49,044 [  17795]   INFO - #c.i.w.i.i.j.s.DelayedProjectSynchronizer$Companion - Workspace model loaded from cache. Syncing real project state into workspace model in 196 ms. Thread[DefaultDispatcher-worker-50,5,main]
2023-05-09 09:05:50,743 [  19494]   INFO - #c.i.v.l.d.i.IndexDiagnosticRunner - Running index diagnostic for [file:////wsl$/Ubuntu/home/marcokrikke/git/test-jdk-idea]
2023-05-09 09:05:51,256 [  20007]   INFO - #o.j.p.g.s.e.GradleExecutionHelper - Passing command-line args to Gradle Tooling API: --init-script C:\Users\Marco.Krikke\AppData\Local\Temp\ijmapper.gradle -Didea.sync.active=true -Didea.resolveSourceSetDependencies=true -Porg.gradle.kotlin.dsl.provider.cid=46684542763400  -Pkotlin.mpp.enableIntransitiveMetadataConfiguration=true --init-script C:\Users\Marco.Krikke\AppData\Local\Temp\ijinit9.gradle
2023-05-09 09:05:51,259 [  20010]   WARN - #o.j.p.g.s.e.GradleExecutionHelper - Host system environment variables will not be passed for the target run.
2023-05-09 09:06:16,872 [  45623]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37631 ms since showing to preload popup menu 'File' at 'MainMenu(preload-bgt)' in 50 ms
2023-05-09 09:06:16,891 [  45642]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37648 ms since showing to preload popup menu 'Window' at 'MainMenu(preload-bgt)' in 68 ms
2023-05-09 09:06:16,903 [  45654]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37659 ms since showing to preload popup menu 'Edit' at 'MainMenu(preload-bgt)' in 80 ms
2023-05-09 09:06:16,954 [  45705]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37711 ms since showing to preload popup menu 'Navigate' at 'MainMenu(preload-bgt)' in 131 ms
2023-05-09 09:06:16,963 [  45714]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37720 ms since showing to preload popup menu 'Run' at 'MainMenu(preload-bgt)' in 141 ms
2023-05-09 09:06:16,968 [  45719]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37725 ms since showing to preload popup menu 'Build' at 'MainMenu(preload-bgt)' in 145 ms
2023-05-09 09:06:17,192 [  45943]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37949 ms since showing to preload popup menu 'Refactor' at 'MainMenu(preload-bgt)' in 369 ms
2023-05-09 09:06:17,225 [  45976]   INFO - #c.i.o.a.i.PopupMenuPreloader - 37982 ms since showing to preload popup menu 'View' at 'MainMenu(preload-bgt)' in 402 ms
2023-05-09 09:06:17,291 [  46042]   INFO - #c.i.o.a.i.PopupMenuPreloader - 38049 ms since showing to preload popup menu 'Code' at 'MainMenu(preload-bgt)' in 468 ms
2023-05-09 09:06:17,378 [  46129]   INFO - #c.i.o.a.i.PopupMenuPreloader - 35320 ms since showing to preload popup menu 'Editor Popup Menu' at 'EditorPopup(preload-bgt)' in 554 ms
2023-05-09 09:06:17,401 [  46152]   INFO - #c.i.o.a.i.PopupMenuPreloader - 35812 ms since showing to preload popup menu 'Editor Popup Menu' at 'EditorPopup(preload-bgt)' in 578 ms
2023-05-09 09:06:20,402 [  49153]   INFO - #c.i.w.i.i.j.s.JpsGlobalModelSynchronizerImpl - Saving global entities to files
2023-05-09 09:06:20,708 [  49459]   INFO - #c.i.c.ComponentStoreImpl - Saving Project(name=test-jdk-idea, containerState=COMPONENT_CREATED, componentStore=\\wsl$\Ubuntu\home\marcokrikke\git\test-jdk-idea)RunManager took 43 ms
2023-05-09 09:06:21,711 [  50462]   INFO - #c.i.e.wsl - WSL mount root for Ubuntu is /mnt/ (done in 275 ms)
2023-05-09 09:06:34,946 [  63697]   INFO - #o.j.p.g.s.p.GradleProjectResolver - Gradle project resolve error
java.lang.IllegalArgumentException: C:\usr\lib\jvm\zulu11-ca-amd64 doesn't exist
	at com.intellij.openapi.projectRoots.impl.JavaSdkImpl.createJdk(JavaSdkImpl.java:404)
	at com.intellij.openapi.externalSystem.service.execution.ExternalSystemJavaSdkProvider.createJdk(ExternalSystemJavaSdkProvider.java:30)
	at org.jetbrains.plugins.gradle.service.project.JavaGradleProjectResolver.lookupSdkByPath(JavaGradleProjectResolver.java:520)
	at org.jetbrains.plugins.gradle.service.project.JavaGradleProjectResolver.populateModuleSdkModel(JavaGradleProjectResolver.java:462)
	at org.jetbrains.plugins.gradle.service.project.JavaGradleProjectResolver.populateJavaModuleCompilerSettings(JavaGradleProjectResolver.java:295)
	at org.jetbrains.plugins.gradle.service.project.JavaGradleProjectResolver.populateModuleExtraModels(JavaGradleProjectResolver.java:83)
	at org.jetbrains.plugins.gradle.service.project.AbstractProjectResolverExtension.populateModuleExtraModels(AbstractProjectResolverExtension.java:85)
	at org.jetbrains.plugins.gradle.service.project.AbstractProjectResolverExtension.populateModuleExtraModels(AbstractProjectResolverExtension.java:85)
	at org.jetbrains.plugins.gradle.service.project.AbstractProjectResolverExtension.populateModuleExtraModels(AbstractProjectResolverExtension.java:85)
	at org.jetbrains.plugins.gradle.service.project.AbstractProjectResolverExtension.populateModuleExtraModels(AbstractProjectResolverExtension.java:85)
	at org.jetbrains.plugins.gradle.service.project.AbstractProjectResolverExtension.populateModuleExtraModels(AbstractProjectResolverExtension.java:85)
	at org.jetbrains.plugins.gradle.service.project.AbstractProjectResolverExtension.populateModuleExtraModels(AbstractProjectResolverExtension.java:85)
	at org.jetbrains.plugins.gradle.service.project.TracedProjectResolverExtension.populateModuleExtraModels(TracedProjectResolverExtension.java:46)
	at org.jetbrains.plugins.gradle.service.project.GradleProjectResolver.convertData(GradleProjectResolver.java:493)
	at org.jetbrains.plugins.gradle.service.project.GradleProjectResolver.doResolveProjectInfo(GradleProjectResolver.java:335)
	at org.jetbrains.plugins.gradle.service.project.GradleProjectResolver$ProjectConnectionDataNodeFunction.fun(GradleProjectResolver.java:860)
	at org.jetbrains.plugins.gradle.service.project.GradleProjectResolver$ProjectConnectionDataNodeFunction.fun(GradleProjectResolver.java:842)
	at org.jetbrains.plugins.gradle.service.execution.GradleExecutionHelper.lambda$execute$0(GradleExecutionHelper.java:131)
	at org.jetbrains.plugins.gradle.service.execution.GradleExecutionHelper.maybeFixSystemProperties(GradleExecutionHelper.java:157)
	at org.jetbrains.plugins.gradle.service.execution.GradleExecutionHelper.lambda$execute$1(GradleExecutionHelper.java:131)
	at org.jetbrains.plugins.gradle.GradleConnectorService$Companion.withGradleConnection(GradleConnectorService.kt:184)
	at org.jetbrains.plugins.gradle.GradleConnectorService.withGradleConnection(GradleConnectorService.kt)
	at org.jetbrains.plugins.gradle.service.execution.GradleExecutionHelper.execute(GradleExecutionHelper.java:127)
	at org.jetbrains.plugins.gradle.service.project.GradleProjectResolver.resolveProjectInfo(GradleProjectResolver.java:160)
	at org.jetbrains.plugins.gradle.service.project.GradleProjectResolver.resolveProjectInfo(GradleProjectResolver.java:76)
	at com.intellij.openapi.externalSystem.service.remote.RemoteExternalSystemProjectResolverImpl.lambda$resolveProjectInfo$0(RemoteExternalSystemProjectResolverImpl.java:35)
	at com.intellij.openapi.externalSystem.service.remote.AbstractRemoteExternalSystemService.execute(AbstractRemoteExternalSystemService.java:40)
	at com.intellij.openapi.externalSystem.service.remote.RemoteExternalSystemProjectResolverImpl.resolveProjectInfo(RemoteExternalSystemProjectResolverImpl.java:34)
	at com.intellij.openapi.externalSystem.service.remote.wrapper.ExternalSystemProjectResolverWrapper.resolveProjectInfo(ExternalSystemProjectResolverWrapper.java:46)
	at com.intellij.openapi.externalSystem.service.internal.ExternalSystemResolveProjectTask.lambda$pauseIndexingAndResolveProjectNode$0(ExternalSystemResolveProjectTask.java:156)
	at com.intellij.openapi.project.MergingQueueGuiSuspender.suspendAndRun(MergingQueueGuiSuspender.java:23)
	at com.intellij.openapi.project.MergingQueueGuiExecutor.suspendAndRun(MergingQueueGuiExecutor.java:281)
	at com.intellij.openapi.project.DumbServiceImpl.suspendIndexingAndRun(DumbServiceImpl.java:187)
	at com.intellij.util.indexing.UnindexedFilesScannerExecutor.lambda$suspendScanningAndIndexingThenRun$0(UnindexedFilesScannerExecutor.java:141)
	at com.intellij.openapi.project.MergingQueueGuiSuspender.suspendAndRun(MergingQueueGuiSuspender.java:23)
	at com.intellij.openapi.project.MergingQueueGuiExecutor.suspendAndRun(MergingQueueGuiExecutor.java:281)
	at com.intellij.util.indexing.UnindexedFilesScannerExecutor.suspendScanningAndIndexingThenRun(UnindexedFilesScannerExecutor.java:140)
	at com.intellij.openapi.externalSystem.service.internal.ExternalSystemResolveProjectTask.pauseIndexingAndResolveProjectNode(ExternalSystemResolveProjectTask.java:154)
	at com.intellij.openapi.externalSystem.service.internal.ExternalSystemResolveProjectTask.doExecute(ExternalSystemResolveProjectTask.java:121)
	at com.intellij.openapi.externalSystem.service.internal.AbstractExternalSystemTask.execute(AbstractExternalSystemTask.java:149)
	at com.intellij.openapi.externalSystem.service.internal.AbstractExternalSystemTask.execute(AbstractExternalSystemTask.java:133)
	at com.intellij.openapi.externalSystem.util.ExternalSystemUtil$2.executeImpl(ExternalSystemUtil.java:499)
	at com.intellij.openapi.externalSystem.util.ExternalSystemUtil$2.execute(ExternalSystemUtil.java:330)
	at com.intellij.openapi.externalSystem.util.ExternalSystemUtil$4.run(ExternalSystemUtil.java:620)
	at com.intellij.openapi.progress.impl.CoreProgressManager.startTask(CoreProgressManager.java:429)
	at com.intellij.openapi.progress.impl.ProgressManagerImpl.startTask(ProgressManagerImpl.java:114)
	at com.intellij.openapi.progress.impl.CoreProgressManager.lambda$runProcessWithProgressAsynchronously$6(CoreProgressManager.java:480)
	at com.intellij.openapi.progress.impl.ProgressRunner.lambda$submit$3(ProgressRunner.java:252)
	at com.intellij.openapi.progress.impl.CoreProgressManager.lambda$runProcess$2(CoreProgressManager.java:186)
	at com.intellij.openapi.progress.impl.CoreProgressManager.lambda$executeProcessUnderProgress$13(CoreProgressManager.java:604)
	at com.intellij.openapi.progress.impl.CoreProgressManager.registerIndicatorAndRun(CoreProgressManager.java:679)
	at com.intellij.openapi.progress.impl.CoreProgressManager.computeUnderProgress(CoreProgressManager.java:635)
	at com.intellij.openapi.progress.impl.CoreProgressManager.executeProcessUnderProgress(CoreProgressManager.java:603)
	at com.intellij.openapi.progress.impl.ProgressManagerImpl.executeProcessUnderProgress(ProgressManagerImpl.java:60)
	at com.intellij.openapi.progress.impl.CoreProgressManager.runProcess(CoreProgressManager.java:173)
	at com.intellij.openapi.progress.impl.ProgressRunner.lambda$submit$4(ProgressRunner.java:252)
	at java.base/java.util.concurrent.CompletableFuture$AsyncSupply.run(CompletableFuture.java:1768)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1136)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:635)
	at java.base/java.util.concurrent.Executors$PrivilegedThreadFactory$1$1.run(Executors.java:702)
	at java.base/java.util.concurrent.Executors$PrivilegedThreadFactory$1$1.run(Executors.java:699)
	at java.base/java.security.AccessController.doPrivileged(AccessController.java:399)
	at java.base/java.util.concurrent.Executors$PrivilegedThreadFactory$1.run(Executors.java:699)
	at java.base/java.lang.Thread.run(Thread.java:833)
2023-05-09 09:06:35,030 [  63781]   INFO - #c.i.o.e.u.ExternalSystemUtil - External project [//wsl$/Ubuntu/home/marcokrikke/git/test-jdk-idea] resolution task executed in 49876 ms.
````
