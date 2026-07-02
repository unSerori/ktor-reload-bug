# Auto-reloadが初回のみ成功し、2回目以降検知されないことがある（3.5.0以降に発生したregression）

## Summary

3.5.0以降で、ホットリロード（`./gradlew -t build`）が、サーバ起動後の最初のソースコード変更&保存では正常に動作しますが、2回目以降の変更では正常に動作しないことがある。

## Expected Behavior

3.4.1以前と同様に、ホットリロードが正常に動作する。

## Description

Summaryのとおり。

ログを添付する。
サーバ起動完了から、1回目の変更&保存と2回目の変更&保存。

<details>
<summary>3.4.3のログ</summary>

```log
> Task :run
2026-07-02 08:24:16.023 [main] INFO  Application - Application started in 0.577 seconds.
2026-07-02 08:24:16.251 [main] INFO  Application - Responding at http://0.0.0.0:8080
modified: /app/src/main/kotlin/Routing.kt
Change detected, executing build...

Operational build model parameters: {cachingModelBuilding=false, configurationCache=false, configurationCacheDisabledReason=null, configurationCacheParallelLoad=false, configurationCacheParallelStore=false, configureOnDemand=false, invalidateCoupledProjects=false, isolatedProjects=false, modelAsProjectDependency=false, modelBuilding=false, parallelModelBuilding=false, parallelProjectConfiguration=false, parallelProjectExecution=false, resilientModelBuilding=false}
Now considering [/app] as hierarchies to watch
Watching the file system is configured to be enabled if available
File system watching is active
Starting Build
Resolved plugin [id: 'org.gradle.toolchains.foojay-resolver-convention', version: '1.0.0']
Settings evaluated using settings file '/app/settings.gradle.kts'.
Projects loaded. Root project using build file '/app/build.gradle.kts'.
Included projects: [root project 'ktor-sample']

> Configure project :
Evaluating root project 'ktor-sample' using build file '/app/build.gradle.kts'.
Resolved plugin [id: 'org.jetbrains.kotlin.jvm', version: '2.4.0']
Resolved plugin [id: 'io.ktor.plugin', version: '3.4.3']
Build 6e8c7720-961a-4cf6-9fa8-5b6973d0cb8b is started
Using Kotlin Gradle Plugin gradle813 variant
kotlin scripting plugin: created the scripting discovery configuration: kotlinScriptDef
kotlin scripting plugin: created the scripting discovery configuration: testKotlinScriptDef
Skipping Develocity integration for Shadow plugin.
Setting org.gradle.jvm.version attribute for shadowRuntimeElements configuration.
Setting target JVM version to 21 for shadowRuntimeElements configuration.
Adding shadowRuntimeElements variant to Java component.
All projects evaluated.
Task name matched 'build'
Selected primary task 'build' from project :
Tasks to be executed: [task ':checkKotlinGradlePluginConfigurationErrors', task ':compileKotlin', task ':compileJava', task ':processResources', task ':classes', task ':jar', task ':startScripts', task ':distTar', task ':distZip', task ':shadowJar', task ':startShadowScripts', task ':shadowDistTar', task ':shadowDistZip', task ':assemble', task ':check', task ':build']
Tasks that were excluded: [task ':test']
Resolve mutations for :checkKotlinGradlePluginConfigurationErrors (Thread[#86,Execution worker,5,main]) started.
:checkKotlinGradlePluginConfigurationErrors (Thread[#86,Execution worker,5,main]) started.

> Task :checkKotlinGradlePluginConfigurationErrors SKIPPED
Skipping task ':checkKotlinGradlePluginConfigurationErrors' as task onlyIf 'errorDiagnostics are present' is false.
Resolve mutations for :compileKotlin (Thread[#86,Execution worker,5,main]) started.
:compileKotlin (Thread[#86,Execution worker,5,main]) started.
Resolve mutations for :processResources (Thread[#89,Execution worker Thread 4,5,main]) started.
:processResources (Thread[#89,Execution worker Thread 4,5,main]) started.

> Task :processResources UP-TO-DATE
Caching disabled for task ':processResources' because:
  Build cache is disabled
  Not worth caching
Skipping task ':processResources' as it is up-to-date.
Resolve mutations for :check (Thread[#89,Execution worker Thread 4,5,main]) started.
:check (Thread[#89,Execution worker Thread 4,5,main]) started.

> Task :check
Skipping task ':check' as it has no actions.

> Task :compileKotlin
Caching disabled for task ':compileKotlin' because:
  Build cache is disabled
Task ':compileKotlin' is not up-to-date because:
  Input property 'sources' file /app/src/main/kotlin/Routing.kt has changed.
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
Kotlin source files: /app/src/main/kotlin/Routing.kt, /app/src/main/kotlin/main.kt
Java source files:
Script source files:
Script file extensions:
Using Kotlin/JVM incremental compilation
[KOTLIN] Kotlin compilation 'jdkHome' argument: /opt/java/openjdk
i: cannot connect to registry: Connection refused
i: starting the daemon as: /opt/java/openjdk/bin/java -cp /root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-compat/2.4.0/209372718c8759fbcb47402dc130d45f00c3f81/kotlin-build-tools-compat-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-impl/2.4.0/3dde5b4075cd7963afd0b0b2835627f40abc1149/kotlin-build-tools-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-tooling-core/2.4.0/75970f5a2a9cb4d25557965bbec0a7ccd55bfbcf/kotlin-tooling-core-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-cri-impl/2.4.0/7fdfe4b4de70b7e6d81c054572e862121aa1603a/kotlin-build-tools-cri-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-runner/2.4.0/d2b2336d493d2d3a8047c826cb27606f67029da8/kotlin-compiler-runner-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-embeddable/2.4.0/f1a24af8bd111a83950236b1aec7a6d72a97e92c/kotlin-compiler-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-api/2.4.0/46429d5887df2d02f33fe11a0c8444c5be5fd8da/kotlin-build-tools-api-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-client/2.4.0/e9080614f98d07554367b7e5810529963e9f43e2/kotlin-daemon-client-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib/2.4.0/4e9f4b531dce5c7dee58ed2de9a8b9a763c8dc6c/kotlin-stdlib-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains/annotations/13.0/919f0dfe192fb4e063e7dacadee7f8bb9a2672a9/annotations-13.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-script-runtime/2.4.0/1de03f0ef3e208ab5f97ee6a587e9b8480447df6/kotlin-script-runtime-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-reflect/1.6.10/1cbe9c92c12a94eea200d23c2bbaedaf3daf5132/kotlin-reflect-1.6.10.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-embeddable/2.4.0/1ecabef3a8ba6a8e25654573d54edb7e4136e903/kotlin-daemon-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlinx/kotlinx-coroutines-core-jvm/1.8.0/ac1dc37a30a93150b704022f8d895ee1bd3a36b3/kotlinx-coroutines-core-jvm-1.8.0.jar -Djava.awt.headless=true -Djava.rmi.server.hostname=127.0.0.1 -Xmx512m -XX:MaxMetaspaceSize=384m -XX:ReservedCodeCacheSize=320m -Dkotlin.environment.keepalive -ea -Dkotlin.daemon.custom.run.files.path.for.tests=/root/.kotlin/daemon -XX:+UseCodeCacheFlushing -XX:+UseParallelGC -Dkotlin.daemon.initiator.marker.file=/tmp/kotlin-compiler-client-13019293551741403230-is-running --add-exports java.base/sun.nio.ch=ALL-UNNAMED org.jetbrains.kotlin.daemon.KotlinCompileDaemon --daemon-logsPath /tmp --daemon-logsFileSizeLimit=1048576 --daemon-logsFileCountLimit=3 --daemon-runFilesPath /root/.kotlin/daemon --daemon-autoshutdownIdleSeconds=7200 --daemon-compilerClasspath /root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-compat/2.4.0/209372718c8759fbcb47402dc130d45f00c3f81/kotlin-build-tools-compat-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-impl/2.4.0/3dde5b4075cd7963afd0b0b2835627f40abc1149/kotlin-build-tools-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-tooling-core/2.4.0/75970f5a2a9cb4d25557965bbec0a7ccd55bfbcf/kotlin-tooling-core-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-cri-impl/2.4.0/7fdfe4b4de70b7e6d81c054572e862121aa1603a/kotlin-build-tools-cri-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-runner/2.4.0/d2b2336d493d2d3a8047c826cb27606f67029da8/kotlin-compiler-runner-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-embeddable/2.4.0/f1a24af8bd111a83950236b1aec7a6d72a97e92c/kotlin-compiler-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-api/2.4.0/46429d5887df2d02f33fe11a0c8444c5be5fd8da/kotlin-build-tools-api-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-client/2.4.0/e9080614f98d07554367b7e5810529963e9f43e2/kotlin-daemon-client-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib/2.4.0/4e9f4b531dce5c7dee58ed2de9a8b9a763c8dc6c/kotlin-stdlib-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains/annotations/13.0/919f0dfe192fb4e063e7dacadee7f8bb9a2672a9/annotations-13.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-script-runtime/2.4.0/1de03f0ef3e208ab5f97ee6a587e9b8480447df6/kotlin-script-runtime-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-reflect/1.6.10/1cbe9c92c12a94eea200d23c2bbaedaf3daf5132/kotlin-reflect-1.6.10.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-embeddable/2.4.0/1ecabef3a8ba6a8e25654573d54edb7e4136e903/kotlin-daemon-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlinx/kotlinx-coroutines-core-jvm/1.8.0/ac1dc37a30a93150b704022f8d895ee1bd3a36b3/kotlinx-coroutines-core-jvm-1.8.0.jar
i: #1 retrying connecting to the daemon
i: Options for KOTLIN DAEMON: IncrementalCompilationOptions(super=CompilationOptions(compilerMode=INCREMENTAL_COMPILER, targetPlatform=JVM, reportCategories=[0], reportSeverity=2, requestedCompilationResults=[0], kotlinScriptExtensions=[], generateCompilerRefIndex=false), sourceChanges=org.jetbrains.kotlin.buildtools.api.SourcesChanges$Known@248eb0d8, classpathChanges=NoChanges, workingDir=/app/build/kotlin/compileKotlin/cacheable, multiModuleICSettings=null, icFeatures=IncrementalCompilationFeatures(usePreciseJavaTracking=true, withAbiSnapshot=false,preciseCompilationResultsBackup=true, keepIncrementalCompilationCachesInMemory=true, enableUnsafeIncrementalCompilationForMultiplatform=false, enableMonotonousIncrementalCompileSetExpansion=true), outputFiles=[/app/build/classes/kotlin/main, /app/build/kotlin/compileKotlin/cacheable, /app/build/kotlin/compileKotlin/local-state])
i: Finished executing kotlin compiler using DAEMON strategy
Resolve mutations for :compileJava (Thread[#86,Execution worker,5,main]) started.
:compileJava (Thread[#86,Execution worker,5,main]) started.

> Task :compileJava NO-SOURCE
Skipping task ':compileJava' as it has no source files and no previous output files.
Resolve mutations for :classes (Thread[#86,Execution worker,5,main]) started.
:classes (Thread[#86,Execution worker,5,main]) started.

> Task :classes UP-TO-DATE
Skipping task ':classes' as it has no actions.
Resolve mutations for :jar (Thread[#86,Execution worker,5,main]) started.
:jar (Thread[#86,Execution worker,5,main]) started.

> Task :jar
Caching disabled for task ':jar' because:
  Build cache is disabled
  Not worth caching
Task ':jar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startScripts (Thread[#86,Execution worker,5,main]) started.
:startScripts (Thread[#86,Execution worker,5,main]) started.

> Task :startScripts
Caching disabled for task ':startScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
Resolve mutations for :distTar (Thread[#86,Execution worker,5,main]) started.
:distTar (Thread[#86,Execution worker,5,main]) started.

> Task :distTar
Caching disabled for task ':distTar' because:
  Build cache is disabled
  Not worth caching
Task ':distTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :distZip (Thread[#86,Execution worker,5,main]) started.
:distZip (Thread[#86,Execution worker,5,main]) started.

> Task :distZip
Caching disabled for task ':distZip' because:
  Build cache is disabled
  Not worth caching
Task ':distZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowJar (Thread[#86,Execution worker,5,main]) started.
:shadowJar (Thread[#86,Execution worker,5,main]) started.

> Task :shadowJar
Custom actions are attached to task ':shadowJar'.
Caching disabled for task ':shadowJar' because:
  Build cache is disabled
Task ':shadowJar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
Adding Multi-Release attribute to the manifest if any dependencies contain it.
Skipping package relocators as auto relocation is disabled.
Relocator count: 0.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startShadowScripts (Thread[#86,Execution worker,5,main]) started.
:startShadowScripts (Thread[#86,Execution worker,5,main]) started.

> Task :startShadowScripts
Caching disabled for task ':startShadowScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startShadowScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-all.jar has changed.
Resolve mutations for :shadowDistTar (Thread[#86,Execution worker,5,main]) started.
:shadowDistTar (Thread[#86,Execution worker,5,main]) started.

> Task :shadowDistTar
Caching disabled for task ':shadowDistTar' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowDistZip (Thread[#86,Execution worker,5,main]) started.
:shadowDistZip (Thread[#86,Execution worker,5,main]) started.

> Task :shadowDistZip
Caching disabled for task ':shadowDistZip' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :assemble (Thread[#86,Execution worker,5,main]) started.
:assemble (Thread[#86,Execution worker,5,main]) started.

> Task :assemble
Skipping task ':assemble' as it has no actions.
Resolve mutations for :build (Thread[#86,Execution worker,5,main]) started.
:build (Thread[#86,Execution worker,5,main]) started.

> Task :build
Skipping task ':build' as it has no actions.
Build 6e8c7720-961a-4cf6-9fa8-5b6973d0cb8b is closed

BUILD SUCCESSFUL in 13s
10 actionable tasks: 9 executed, 1 up-to-date
Consider enabling configuration cache to speed up this build: https://docs.gradle.org/9.5.1/userguide/configuration_cache_enabling.html

Waiting for changes to input files...
2026-07-02 08:24:54.723 [eventLoopGroupProxy-3-1] INFO  Application - Changes in application detected.
2026-07-02 08:24:55.031 [eventLoopGroupProxy-3-1] INFO  Application - Application auto-reloaded in 0.036 seconds.
modified: /app/src/main/kotlin/Routing.kt
Change detected, executing build...

Operational build model parameters: {cachingModelBuilding=false, configurationCache=false, configurationCacheDisabledReason=null, configurationCacheParallelLoad=false, configurationCacheParallelStore=false, configureOnDemand=false, invalidateCoupledProjects=false, isolatedProjects=false, modelAsProjectDependency=false, modelBuilding=false, parallelModelBuilding=false, parallelProjectConfiguration=false, parallelProjectExecution=false, resilientModelBuilding=false}
Now considering [/app] as hierarchies to watch
Watching the file system is configured to be enabled if available
File system watching is active
Starting Build
Resolved plugin [id: 'org.gradle.toolchains.foojay-resolver-convention', version: '1.0.0']
Settings evaluated using settings file '/app/settings.gradle.kts'.
Projects loaded. Root project using build file '/app/build.gradle.kts'.
Included projects: [root project 'ktor-sample']

> Configure project :
Evaluating root project 'ktor-sample' using build file '/app/build.gradle.kts'.
Resolved plugin [id: 'org.jetbrains.kotlin.jvm', version: '2.4.0']
Resolved plugin [id: 'io.ktor.plugin', version: '3.4.3']
Build aeb3e08a-aa9a-4ce9-a97b-4c9c41620ae1 is started
Using Kotlin Gradle Plugin gradle813 variant
kotlin scripting plugin: created the scripting discovery configuration: kotlinScriptDef
kotlin scripting plugin: created the scripting discovery configuration: testKotlinScriptDef
Skipping Develocity integration for Shadow plugin.
Setting org.gradle.jvm.version attribute for shadowRuntimeElements configuration.
Setting target JVM version to 21 for shadowRuntimeElements configuration.
Adding shadowRuntimeElements variant to Java component.
All projects evaluated.
Task name matched 'build'
Selected primary task 'build' from project :
Tasks to be executed: [task ':checkKotlinGradlePluginConfigurationErrors', task ':compileKotlin', task ':compileJava', task ':processResources', task ':classes', task ':jar', task ':startScripts', task ':distTar', task ':distZip', task ':shadowJar', task ':startShadowScripts', task ':shadowDistTar', task ':shadowDistZip', task ':assemble', task ':check', task ':build']
Tasks that were excluded: [task ':test']
Resolve mutations for :checkKotlinGradlePluginConfigurationErrors (Thread[#109,Execution worker,5,main]) started.
:checkKotlinGradlePluginConfigurationErrors (Thread[#109,Execution worker,5,main]) started.

> Task :checkKotlinGradlePluginConfigurationErrors SKIPPED
Skipping task ':checkKotlinGradlePluginConfigurationErrors' as task onlyIf 'errorDiagnostics are present' is false.
Resolve mutations for :compileKotlin (Thread[#109,Execution worker,5,main]) started.
:compileKotlin (Thread[#109,Execution worker,5,main]) started.
Resolve mutations for :processResources (Thread[#110,Execution worker Thread 2,5,main]) started.
:processResources (Thread[#110,Execution worker Thread 2,5,main]) started.

> Task :processResources UP-TO-DATE
Caching disabled for task ':processResources' because:
  Build cache is disabled
  Not worth caching
Skipping task ':processResources' as it is up-to-date.
Resolve mutations for :check (Thread[#116,Execution worker Thread 7,5,main]) started.
:check (Thread[#116,Execution worker Thread 7,5,main]) started.

> Task :check
Skipping task ':check' as it has no actions.

> Task :compileKotlin
Caching disabled for task ':compileKotlin' because:
  Build cache is disabled
Task ':compileKotlin' is not up-to-date because:
  Input property 'sources' file /app/src/main/kotlin/Routing.kt has changed.
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
Kotlin source files: /app/src/main/kotlin/Routing.kt, /app/src/main/kotlin/main.kt
Java source files:
Script source files:
Script file extensions:
Using Kotlin/JVM incremental compilation
[KOTLIN] Kotlin compilation 'jdkHome' argument: /opt/java/openjdk
i: Options for KOTLIN DAEMON: IncrementalCompilationOptions(super=CompilationOptions(compilerMode=INCREMENTAL_COMPILER, targetPlatform=JVM, reportCategories=[0], reportSeverity=2, requestedCompilationResults=[0], kotlinScriptExtensions=[], generateCompilerRefIndex=false), sourceChanges=org.jetbrains.kotlin.buildtools.api.SourcesChanges$Known@e575559, classpathChanges=NoChanges, workingDir=/app/build/kotlin/compileKotlin/cacheable, multiModuleICSettings=null, icFeatures=IncrementalCompilationFeatures(usePreciseJavaTracking=true, withAbiSnapshot=false, preciseCompilationResultsBackup=true, keepIncrementalCompilationCachesInMemory=true, enableUnsafeIncrementalCompilationForMultiplatform=false, enableMonotonousIncrementalCompileSetExpansion=true), outputFiles=[/app/build/classes/kotlin/main, /app/build/kotlin/compileKotlin/cacheable, /app/build/kotlin/compileKotlin/local-state])
i: Finished executing kotlin compiler using DAEMON strategy
Resolve mutations for :compileJava (Thread[#109,Execution worker,5,main]) started.
:compileJava (Thread[#109,Execution worker,5,main]) started.

> Task :compileJava NO-SOURCE
Skipping task ':compileJava' as it has no source files and no previous output files.
Resolve mutations for :classes (Thread[#109,Execution worker,5,main]) started.
:classes (Thread[#108,included builds,5,main]) started.

> Task :classes UP-TO-DATE
Skipping task ':classes' as it has no actions.
Resolve mutations for :jar (Thread[#108,included builds,5,main]) started.
:jar (Thread[#108,included builds,5,main]) started.

> Task :jar
Caching disabled for task ':jar' because:
  Build cache is disabled
  Not worth caching
Task ':jar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startScripts (Thread[#108,included builds,5,main]) started.
:startScripts (Thread[#108,included builds,5,main]) started.

> Task :startScripts
Caching disabled for task ':startScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
Resolve mutations for :distTar (Thread[#108,included builds,5,main]) started.
:distTar (Thread[#108,included builds,5,main]) started.

> Task :distTar
Caching disabled for task ':distTar' because:
  Build cache is disabled
  Not worth caching
Task ':distTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :distZip (Thread[#108,included builds,5,main]) started.
:distZip (Thread[#108,included builds,5,main]) started.

> Task :distZip
Caching disabled for task ':distZip' because:
  Build cache is disabled
  Not worth caching
Task ':distZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowJar (Thread[#108,included builds,5,main]) started.
:shadowJar (Thread[#108,included builds,5,main]) started.

> Task :shadowJar
Custom actions are attached to task ':shadowJar'.
Caching disabled for task ':shadowJar' because:
  Build cache is disabled
Task ':shadowJar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
Adding Multi-Release attribute to the manifest if any dependencies contain it.
Skipping package relocators as auto relocation is disabled.
Relocator count: 0.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startShadowScripts (Thread[#108,included builds,5,main]) started.
:startShadowScripts (Thread[#108,included builds,5,main]) started.

> Task :startShadowScripts
Caching disabled for task ':startShadowScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startShadowScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-all.jar has changed.
Resolve mutations for :shadowDistTar (Thread[#108,included builds,5,main]) started.
:shadowDistTar (Thread[#108,included builds,5,main]) started.

> Task :shadowDistTar
Caching disabled for task ':shadowDistTar' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowDistZip (Thread[#108,included builds,5,main]) started.
:shadowDistZip (Thread[#108,included builds,5,main]) started.

> Task :shadowDistZip
Caching disabled for task ':shadowDistZip' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :assemble (Thread[#108,included builds,5,main]) started.
:assemble (Thread[#108,included builds,5,main]) started.

> Task :assemble
Skipping task ':assemble' as it has no actions.
Resolve mutations for :build (Thread[#108,included builds,5,main]) started.
:build (Thread[#108,included builds,5,main]) started.

> Task :build
Skipping task ':build' as it has no actions.
Build aeb3e08a-aa9a-4ce9-a97b-4c9c41620ae1 is closed

BUILD SUCCESSFUL in 8s
10 actionable tasks: 9 executed, 1 up-to-date
Consider enabling configuration cache to speed up this build: https://docs.gradle.org/9.5.1/userguide/configuration_cache_enabling.html

Waiting for changes to input files...
2026-07-02 08:26:28.200 [eventLoopGroupProxy-3-1] INFO  Application - Changes in application detected.
2026-07-02 08:26:28.820 [eventLoopGroupProxy-3-1] INFO  Application - Application auto-reloaded in 0.183 seconds.
```

</details>

<details>
<summary>3.5.0のログ</summary>

```log
> Task :run
2026-07-02 07:42:50.953 [main] INFO  Application - Application started in 0.694 seconds.
2026-07-02 07:42:51.134 [main] INFO  Application - Responding at http://0.0.0.0:8080
modified: /app/src/main/kotlin/Routing.kt
Change detected, executing build...

Operational build model parameters: {cachingModelBuilding=false, configurationCache=false, configurationCacheDisabledReason=null, configurationCacheParallelLoad=false, configurationCacheParallelStore=false, configureOnDemand=false, invalidateCoupledProjects=false, isolatedProjects=false, modelAsProjectDependency=false, modelBuilding=false, parallelModelBuilding=false, parallelProjectConfiguration=false, parallelProjectExecution=false, resilientModelBuilding=false}
Invalidating in-memory cache of /app/.gradle/buildOutputCleanup/outputFiles.bin
Now considering [/app] as hierarchies to watch
Watching the file system is configured to be enabled if available
File system watching is active
Starting Build
Resolved plugin [id: 'org.gradle.toolchains.foojay-resolver-convention', version: '1.0.0']
Invalidating in-memory cache of /root/.gradle/caches/journal-1/file-access.bin
Invalidating in-memory cache of /root/.gradle/caches/9.5.1/fileHashes/kotlinDslCompileAvoidanceClasspathHashCache.bin
Invalidating in-memory cache of /root/.gradle/caches/9.5.1/fileHashes/fileHashes.bin
Invalidating in-memory cache of /root/.gradle/caches/9.5.1/fileHashes/KotlinMetadataCompatibilityCache.bin
Invalidating in-memory cache of /root/.gradle/caches/9.5.1/fileHashes/resourceHashesCache.bin
Settings evaluated using settings file '/app/settings.gradle.kts'.
Projects loaded. Root project using build file '/app/build.gradle.kts'.
Included projects: [root project 'ktor-sample']

> Configure project :
Evaluating root project 'ktor-sample' using build file '/app/build.gradle.kts'.
Resolved plugin [id: 'org.jetbrains.kotlin.jvm', version: '2.4.0']
Resolved plugin [id: 'io.ktor.plugin', version: '3.5.0']
Build da3616a3-351d-4b26-927b-1570891f18e1 is started
Using Kotlin Gradle Plugin gradle813 variant
kotlin scripting plugin: created the scripting discovery configuration: kotlinScriptDef
kotlin scripting plugin: created the scripting discovery configuration: testKotlinScriptDef
Skipping Develocity integration for Shadow plugin.
Setting org.gradle.jvm.version attribute for shadowRuntimeElements configuration.
Setting target JVM version to 21 for shadowRuntimeElements configuration.
Adding shadowRuntimeElements variant to Java component.
All projects evaluated.
Task name matched 'build'
Selected primary task 'build' from project :
Tasks to be executed: [task ':checkKotlinGradlePluginConfigurationErrors', task ':compileKotlin', task ':compileJava', task ':processResources', task ':classes', task ':jar', task ':startScripts', task ':distTar', task ':distZip', task ':shadowJar', task ':startShadowScripts', task ':shadowDistTar', task ':shadowDistZip', task ':assemble', task ':check', task ':build']
Tasks that were excluded: [task ':test']
Resolve mutations for :checkKotlinGradlePluginConfigurationErrors (Thread[#86,Execution worker,5,main]) started.
:checkKotlinGradlePluginConfigurationErrors (Thread[#86,Execution worker,5,main]) started.
Invalidating in-memory cache of /app/.gradle/9.5.1/executionHistory/executionHistory.bin

> Task :checkKotlinGradlePluginConfigurationErrors SKIPPED
Skipping task ':checkKotlinGradlePluginConfigurationErrors' as task onlyIf 'errorDiagnostics are present' is false.
Resolve mutations for :compileKotlin (Thread[#86,Execution worker,5,main]) started.
:compileKotlin (Thread[#86,Execution worker,5,main]) started.
Resolve mutations for :processResources (Thread[#91,Execution worker Thread 6,5,main]) started.
:processResources (Thread[#91,Execution worker Thread 6,5,main]) started.

> Task :processResources UP-TO-DATE
Caching disabled for task ':processResources' because:
  Build cache is disabled
  Not worth caching
Skipping task ':processResources' as it is up-to-date.
Resolve mutations for :check (Thread[#91,Execution worker Thread 6,5,main]) started.
:check (Thread[#91,Execution worker Thread 6,5,main]) started.

> Task :check
Skipping task ':check' as it has no actions.

> Task :compileKotlin
Invalidating in-memory cache of /app/.gradle/9.5.1/fileHashes/fileHashes.bin
Invalidating in-memory cache of /app/.gradle/9.5.1/fileHashes/resourceHashesCache.bin
Caching disabled for task ':compileKotlin' because:
  Build cache is disabled
Task ':compileKotlin' is not up-to-date because:
  Input property 'sources' file /app/src/main/kotlin/Routing.kt has changed.
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
Kotlin source files: /app/src/main/kotlin/Routing.kt, /app/src/main/kotlin/main.kt
Java source files:
Script source files:
Script file extensions:
Using Kotlin/JVM incremental compilation
[KOTLIN] Kotlin compilation 'jdkHome' argument: /opt/java/openjdk
i: cannot connect to registry: Connection refused
i: starting the daemon as: /opt/java/openjdk/bin/java -cp /root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-compat/2.4.0/209372718c8759fbcb47402dc130d45f00c3f81/kotlin-build-tools-compat-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-impl/2.4.0/3dde5b4075cd7963afd0b0b2835627f40abc1149/kotlin-build-tools-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-tooling-core/2.4.0/75970f5a2a9cb4d25557965bbec0a7ccd55bfbcf/kotlin-tooling-core-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-cri-impl/2.4.0/7fdfe4b4de70b7e6d81c054572e862121aa1603a/kotlin-build-tools-cri-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-runner/2.4.0/d2b2336d493d2d3a8047c826cb27606f67029da8/kotlin-compiler-runner-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-embeddable/2.4.0/f1a24af8bd111a83950236b1aec7a6d72a97e92c/kotlin-compiler-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-api/2.4.0/46429d5887df2d02f33fe11a0c8444c5be5fd8da/kotlin-build-tools-api-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-client/2.4.0/e9080614f98d07554367b7e5810529963e9f43e2/kotlin-daemon-client-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib/2.4.0/4e9f4b531dce5c7dee58ed2de9a8b9a763c8dc6c/kotlin-stdlib-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains/annotations/13.0/919f0dfe192fb4e063e7dacadee7f8bb9a2672a9/annotations-13.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-script-runtime/2.4.0/1de03f0ef3e208ab5f97ee6a587e9b8480447df6/kotlin-script-runtime-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-reflect/1.6.10/1cbe9c92c12a94eea200d23c2bbaedaf3daf5132/kotlin-reflect-1.6.10.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-embeddable/2.4.0/1ecabef3a8ba6a8e25654573d54edb7e4136e903/kotlin-daemon-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlinx/kotlinx-coroutines-core-jvm/1.8.0/ac1dc37a30a93150b704022f8d895ee1bd3a36b3/kotlinx-coroutines-core-jvm-1.8.0.jar -Djava.awt.headless=true -Djava.rmi.server.hostname=127.0.0.1 -Xmx512m -XX:MaxMetaspaceSize=384m -XX:ReservedCodeCacheSize=320m -Dkotlin.environment.keepalive -ea -Dkotlin.daemon.custom.run.files.path.for.tests=/root/.kotlin/daemon -XX:+UseCodeCacheFlushing -XX:+UseParallelGC -Dkotlin.daemon.initiator.marker.file=/tmp/kotlin-compiler-client-3030009259462559364-is-running --add-exports java.base/sun.nio.ch=ALL-UNNAMED org.jetbrains.kotlin.daemon.KotlinCompileDaemon --daemon-logsPath /tmp --daemon-logsFileSizeLimit=1048576 --daemon-logsFileCountLimit=3 --daemon-runFilesPath /root/.kotlin/daemon --daemon-autoshutdownIdleSeconds=7200 --daemon-compilerClasspath /root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-compat/2.4.0/209372718c8759fbcb47402dc130d45f00c3f81/kotlin-build-tools-compat-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-impl/2.4.0/3dde5b4075cd7963afd0b0b2835627f40abc1149/kotlin-build-tools-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-tooling-core/2.4.0/75970f5a2a9cb4d25557965bbec0a7ccd55bfbcf/kotlin-tooling-core-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-cri-impl/2.4.0/7fdfe4b4de70b7e6d81c054572e862121aa1603a/kotlin-build-tools-cri-impl-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-runner/2.4.0/d2b2336d493d2d3a8047c826cb27606f67029da8/kotlin-compiler-runner-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-compiler-embeddable/2.4.0/f1a24af8bd111a83950236b1aec7a6d72a97e92c/kotlin-compiler-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-build-tools-api/2.4.0/46429d5887df2d02f33fe11a0c8444c5be5fd8da/kotlin-build-tools-api-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-client/2.4.0/e9080614f98d07554367b7e5810529963e9f43e2/kotlin-daemon-client-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-stdlib/2.4.0/4e9f4b531dce5c7dee58ed2de9a8b9a763c8dc6c/kotlin-stdlib-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains/annotations/13.0/919f0dfe192fb4e063e7dacadee7f8bb9a2672a9/annotations-13.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-script-runtime/2.4.0/1de03f0ef3e208ab5f97ee6a587e9b8480447df6/kotlin-script-runtime-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-reflect/1.6.10/1cbe9c92c12a94eea200d23c2bbaedaf3daf5132/kotlin-reflect-1.6.10.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlin/kotlin-daemon-embeddable/2.4.0/1ecabef3a8ba6a8e25654573d54edb7e4136e903/kotlin-daemon-embeddable-2.4.0.jar:/root/.gradle/caches/modules-2/files-2.1/org.jetbrains.kotlinx/kotlinx-coroutines-core-jvm/1.8.0/ac1dc37a30a93150b704022f8d895ee1bd3a36b3/kotlinx-coroutines-core-jvm-1.8.0.jar
i: #1 retrying connecting to the daemon
i: cannot connect to registry: Connection refused
i: Options for KOTLIN DAEMON: IncrementalCompilationOptions(super=CompilationOptions(compilerMode=INCREMENTAL_COMPILER, targetPlatform=JVM, reportCategories=[0], reportSeverity=2, requestedCompilationResults=[0], kotlinScriptExtensions=[], generateCompilerRefIndex=false), sourceChanges=org.jetbrains.kotlin.buildtools.api.SourcesChanges$Known@4dc4ea9c,classpathChanges=NoChanges, workingDir=/app/build/kotlin/compileKotlin/cacheable, multiModuleICSettings=null, icFeatures=IncrementalCompilationFeatures(usePreciseJavaTracking=true, withAbiSnapshot=false, preciseCompilationResultsBackup=true, keepIncrementalCompilationCachesInMemory=true, enableUnsafeIncrementalCompilationForMultiplatform=false, enableMonotonousIncrementalCompileSetExpansion=true), outputFiles=[/app/build/classes/kotlin/main, /app/build/kotlin/compileKotlin/cacheable, /app/build/kotlin/compileKotlin/local-state])
i: Finished executing kotlin compiler using DAEMON strategy
Resolve mutations for :compileJava (Thread[#86,Execution worker,5,main]) started.
:compileJava (Thread[#86,Execution worker,5,main]) started.

> Task :compileJava NO-SOURCE
Skipping task ':compileJava' as it has no source files and no previous output files.
Resolve mutations for :classes (Thread[#86,Execution worker,5,main]) started.
:classes (Thread[#86,Execution worker,5,main]) started.

> Task :classes UP-TO-DATE
Skipping task ':classes' as it has no actions.
Resolve mutations for :jar (Thread[#86,Execution worker,5,main]) started.
:jar (Thread[#86,Execution worker,5,main]) started.

> Task :jar
Caching disabled for task ':jar' because:
  Build cache is disabled
  Not worth caching
Task ':jar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startScripts (Thread[#86,Execution worker,5,main]) started.
:startScripts (Thread[#86,Execution worker,5,main]) started.

> Task :startScripts
Caching disabled for task ':startScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
Resolve mutations for :distTar (Thread[#86,Execution worker,5,main]) started.
:distTar (Thread[#86,Execution worker,5,main]) started.

> Task :distTar
Caching disabled for task ':distTar' because:
  Build cache is disabled
  Not worth caching
Task ':distTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :distZip (Thread[#86,Execution worker,5,main]) started.
:distZip (Thread[#86,Execution worker,5,main]) started.

> Task :distZip
Caching disabled for task ':distZip' because:
  Build cache is disabled
  Not worth caching
Task ':distZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowJar (Thread[#86,Execution worker,5,main]) started.
:shadowJar (Thread[#86,Execution worker,5,main]) started.

> Task :shadowJar
Custom actions are attached to task ':shadowJar'.
Caching disabled for task ':shadowJar' because:
  Build cache is disabled
Task ':shadowJar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
Adding Multi-Release attribute to the manifest if any dependencies contain it.
Skipping package relocators as auto relocation is disabled.
Relocator count: 0.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startShadowScripts (Thread[#86,Execution worker,5,main]) started.
:startShadowScripts (Thread[#86,Execution worker,5,main]) started.

> Task :startShadowScripts
Caching disabled for task ':startShadowScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startShadowScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-all.jar has changed.
Resolve mutations for :shadowDistTar (Thread[#86,Execution worker,5,main]) started.
:shadowDistTar (Thread[#86,Execution worker,5,main]) started.

> Task :shadowDistTar
Caching disabled for task ':shadowDistTar' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowDistZip (Thread[#86,Execution worker,5,main]) started.
:shadowDistZip (Thread[#86,Execution worker,5,main]) started.

> Task :shadowDistZip
Caching disabled for task ':shadowDistZip' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :assemble (Thread[#86,Execution worker,5,main]) started.
:assemble (Thread[#86,Execution worker,5,main]) started.

> Task :assemble
Skipping task ':assemble' as it has no actions.
Resolve mutations for :build (Thread[#86,Execution worker,5,main]) started.
:build (Thread[#86,Execution worker,5,main]) started.

> Task :build
Skipping task ':build' as it has no actions.
Build da3616a3-351d-4b26-927b-1570891f18e1 is closed

BUILD SUCCESSFUL in 13s
10 actionable tasks: 9 executed, 1 up-to-date
Consider enabling configuration cache to speed up this build: https://docs.gradle.org/9.5.1/userguide/configuration_cache_enabling.html

Waiting for changes to input files...
2026-07-02 07:43:32.377 [eventLoopGroupProxy-3-1] INFO  Application - Changes in application detected.
2026-07-02 07:43:32.696 [eventLoopGroupProxy-3-1] INFO  Application - Application auto-reloaded in 0.015 seconds.
modified: /app/src/main/kotlin/Routing.kt
Change detected, executing build...

Operational build model parameters: {cachingModelBuilding=false, configurationCache=false, configurationCacheDisabledReason=null, configurationCacheParallelLoad=false, configurationCacheParallelStore=false, configureOnDemand=false, invalidateCoupledProjects=false, isolatedProjects=false, modelAsProjectDependency=false, modelBuilding=false, parallelModelBuilding=false, parallelProjectConfiguration=false, parallelProjectExecution=false, resilientModelBuilding=false}
Now considering [/app] as hierarchies to watch
Watching the file system is configured to be enabled if available
File system watching is active
Starting Build
Resolved plugin [id: 'org.gradle.toolchains.foojay-resolver-convention', version: '1.0.0']
Settings evaluated using settings file '/app/settings.gradle.kts'.
Projects loaded. Root project using build file '/app/build.gradle.kts'.
Included projects: [root project 'ktor-sample']

> Configure project :
Evaluating root project 'ktor-sample' using build file '/app/build.gradle.kts'.
Resolved plugin [id: 'org.jetbrains.kotlin.jvm', version: '2.4.0']
Resolved plugin [id: 'io.ktor.plugin', version: '3.5.0']
Build 6c1de52d-5979-4b92-8af9-41c6c7a61b2c is started
Using Kotlin Gradle Plugin gradle813 variant
kotlin scripting plugin: created the scripting discovery configuration: kotlinScriptDef
kotlin scripting plugin: created the scripting discovery configuration: testKotlinScriptDef
Skipping Develocity integration for Shadow plugin.
Setting org.gradle.jvm.version attribute for shadowRuntimeElements configuration.
Setting target JVM version to 21 for shadowRuntimeElements configuration.
Adding shadowRuntimeElements variant to Java component.
All projects evaluated.
Task name matched 'build'
Selected primary task 'build' from project :
Tasks to be executed: [task ':checkKotlinGradlePluginConfigurationErrors', task ':compileKotlin', task ':compileJava', task ':processResources', task ':classes', task ':jar', task ':startScripts', task ':distTar', task ':distZip', task ':shadowJar', task ':startShadowScripts', task ':shadowDistTar', task ':shadowDistZip', task ':assemble', task ':check', task ':build']
Tasks that were excluded: [task ':test']
Resolve mutations for :checkKotlinGradlePluginConfigurationErrors (Thread[#109,Execution worker,5,main]) started.
:checkKotlinGradlePluginConfigurationErrors (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :checkKotlinGradlePluginConfigurationErrors SKIPPED
Skipping task ':checkKotlinGradlePluginConfigurationErrors' as task onlyIf 'errorDiagnostics are present' is false.
Resolve mutations for :compileKotlin (Thread[#111,Execution worker Thread 3,5,main]) started.
:compileKotlin (Thread[#111,Execution worker Thread 3,5,main]) started.
Resolve mutations for :processResources (Thread[#109,Execution worker,5,main]) started.
:processResources (Thread[#109,Execution worker,5,main]) started.

> Task :processResources UP-TO-DATE
Caching disabled for task ':processResources' because:
  Build cache is disabled
  Not worth caching
Skipping task ':processResources' as it is up-to-date.
Resolve mutations for :check (Thread[#109,Execution worker,5,main]) started.
:check (Thread[#109,Execution worker,5,main]) started.

> Task :check
Skipping task ':check' as it has no actions.

> Task :compileKotlin
Caching disabled for task ':compileKotlin' because:
  Build cache is disabled
Task ':compileKotlin' is not up-to-date because:
  Input property 'sources' file /app/src/main/kotlin/Routing.kt has changed.
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
file or directory '/app/src/main/java', not found
Kotlin source files: /app/src/main/kotlin/Routing.kt, /app/src/main/kotlin/main.kt
Java source files:
Script source files:
Script file extensions:
Using Kotlin/JVM incremental compilation
[KOTLIN] Kotlin compilation 'jdkHome' argument: /opt/java/openjdk
i: cannot connect to registry: Connection refused
i: Options for KOTLIN DAEMON: IncrementalCompilationOptions(super=CompilationOptions(compilerMode=INCREMENTAL_COMPILER, targetPlatform=JVM, reportCategories=[0], reportSeverity=2, requestedCompilationResults=[0], kotlinScriptExtensions=[], generateCompilerRefIndex=false), sourceChanges=org.jetbrains.kotlin.buildtools.api.SourcesChanges$Known@3e54fdc, classpathChanges=NoChanges, workingDir=/app/build/kotlin/compileKotlin/cacheable, multiModuleICSettings=null, icFeatures=IncrementalCompilationFeatures(usePreciseJavaTracking=true, withAbiSnapshot=false, preciseCompilationResultsBackup=true, keepIncrementalCompilationCachesInMemory=true, enableUnsafeIncrementalCompilationForMultiplatform=false, enableMonotonousIncrementalCompileSetExpansion=true), outputFiles=[/app/build/classes/kotlin/main, /app/build/kotlin/compileKotlin/cacheable, /app/build/kotlin/compileKotlin/local-state])
i: Finished executing kotlin compiler using DAEMON strategy
Resolve mutations for :compileJava (Thread[#111,Execution worker Thread 3,5,main]) started.
:compileJava (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :compileJava NO-SOURCE
Skipping task ':compileJava' as it has no source files and no previous output files.
Resolve mutations for :classes (Thread[#111,Execution worker Thread 3,5,main]) started.
:classes (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :classes UP-TO-DATE
Skipping task ':classes' as it has no actions.
Resolve mutations for :jar (Thread[#111,Execution worker Thread 3,5,main]) started.
:jar (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :jar
Caching disabled for task ':jar' because:
  Build cache is disabled
  Not worth caching
Task ':jar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startScripts (Thread[#111,Execution worker Thread 3,5,main]) started.
:startScripts (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :startScripts
Caching disabled for task ':startScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
Resolve mutations for :distTar (Thread[#111,Execution worker Thread 3,5,main]) started.
:distTar (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :distTar
Caching disabled for task ':distTar' because:
  Build cache is disabled
  Not worth caching
Task ':distTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :distZip (Thread[#111,Execution worker Thread 3,5,main]) started.
:distZip (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :distZip
Caching disabled for task ':distZip' because:
  Build cache is disabled
  Not worth caching
Task ':distZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1$1' file /app/build/libs/ktor-sample-1.0.0-SNAPSHOT.jar has changed.
file or directory '/app/src/main/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowJar (Thread[#111,Execution worker Thread 3,5,main]) started.
:shadowJar (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :shadowJar
Custom actions are attached to task ':shadowJar'.
Caching disabled for task ':shadowJar' because:
  Build cache is disabled
Task ':shadowJar' is not up-to-date because:
  Input property 'rootSpec$1' file /app/build/classes/kotlin/main/com/example/RoutingKt$configureRouting$1$1.class has changed.
Adding Multi-Release attribute to the manifest if any dependencies contain it.
Skipping package relocators as auto relocation is disabled.
Relocator count: 0.
file or directory '/app/build/classes/java/main', not found
Resolve mutations for :startShadowScripts (Thread[#111,Execution worker Thread 3,5,main]) started.
:startShadowScripts (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :startShadowScripts
Caching disabled for task ':startShadowScripts' because:
  Build cache is disabled
  Not worth caching
Task ':startShadowScripts' is not up-to-date because:
  Input property 'classpath' file /app/build/libs/ktor-sample-all.jar has changed.
Resolve mutations for :shadowDistTar (Thread[#111,Execution worker Thread 3,5,main]) started.
:shadowDistTar (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :shadowDistTar
Caching disabled for task ':shadowDistTar' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistTar' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :shadowDistZip (Thread[#111,Execution worker Thread 3,5,main]) started.
:shadowDistZip (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :shadowDistZip
Caching disabled for task ':shadowDistZip' because:
  Build cache is disabled
  Not worth caching
Task ':shadowDistZip' is not up-to-date because:
  Input property 'rootSpec$1$1$1$1' file /app/build/libs/ktor-sample-all.jar has changed.
file or directory '/app/src/shadow/dist', not found
file or directory '/app/src/dist', not found
Resolve mutations for :assemble (Thread[#111,Execution worker Thread 3,5,main]) started.
:assemble (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :assemble
Skipping task ':assemble' as it has no actions.
Resolve mutations for :build (Thread[#111,Execution worker Thread 3,5,main]) started.
:build (Thread[#111,Execution worker Thread 3,5,main]) started.

> Task :build
Skipping task ':build' as it has no actions.
Build 6c1de52d-5979-4b92-8af9-41c6c7a61b2c is closed

BUILD SUCCESSFUL in 7s
10 actionable tasks: 9 executed, 1 up-to-date
Consider enabling configuration cache to speed up this build: https://docs.gradle.org/9.5.1/userguide/configuration_cache_enabling.html

Waiting for changes to input files...
```

</details>

2回目であっても、

- 保存そのものには反応してログが流れている。
- BUILD SUCCESSFUL自体は表示されている
- 二度目の変更&保存後にリクエストを送ると、「Waiting for changes to input files...」以降に流れるべき「Application - Changes in application detected. Application - Application auto-reloaded in 0.000 seconds.」が流れない。Ktorはアクセス時に更新するという認識。

なお、サーバを再起動すると、同じ問題が発生する。

## Steps to Reproduce

1. [start.ktor.io](https://start.ktor.io/)でシンプルなプロジェクトを取得
   - Build system: Gradle
   - Engine: Netty
   - Configuration: HOCON File
2. [公式のAuto-reload](https://ktor.io/docs/server-auto-reload.html)どおりの設定・編集を行う
3. 紹介されている`./gradlew -t build -x test -i`を使い変更を監視し、`./gradlew run`でサーバを立ち上げる
4. 適当にコードを変更&保存

各種バージョンでの検証を行うための[シンプルなリポジトリ](https://github.com/unSerori/ktor-reload-bug)を公開しています

## Investigation Note

最初に「Kotlin: 2.4.0, Ktor: 3.5.0」プロジェクトを立ち上げる過程でうまく動作しないことに気づいた。
調査した結果、この[「Kotlin: 2.1.10, Ktor: 3.2.2」なサンプル](https://github.com/Tomoki108/ktor-sample)を見つけたため、過去のバージョンで動作していることは確認できた。

次に、KotlinとKtorどちらが原因かを調査するため、「Kotlin: 2.1.10, Ktor: 3.5.0」と「Kotlin: 2.4.0, Ktor: 3.2.2」で確認した。
前者はそもそもkotlinバージョンに対してktorのバージョンが高いようでビルドが通らない、後者は動作した。
そのため、Kotlinのバージョン2.4.0が問題なのではなく、Ktor3.5.0付近が問題でありそうだとした。

最後に、Ktorの3.2.2~3.5.0バージョンを二分探査で調査した。
結果は以下

| Kotlin Version | Ktor Version                             | 結果                                                                                                                          |
| -------------- | ---------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| 2.1.10         | 3.2.2                                    | 正常に動作した                                                                                                                |
| 2.1.10         | 3.5.1                                    | そもそもkotlinバージョンに対してktorのバージョンが高いようでビルドが通らない（Kotlin Metadataの非互換であり、今回は関係ない） |
| 2.4.0          | 3.2.2                                    | 正常に動作した->Kotlin 2.4.0は問題ではなさそう                                                                                |
| 2.4.0          | 3.3.3, 3.4.0, 3.4.1, 3.4.2, 3.4.3, 3.4.1 | 正常に動作した                                                                                                                |
| 2.4.0          | 3.5.0                                    | 正常に動作しなかった                                                                                                          |
| 2.4.0          | 3.5.1                                    | 正常に動作しなかった                                                                                                          |

3.4.1までは正常動作、3.5.0から動作しなくなっている。
念の為、3.5.1でも試したが、同様の問題が確認された。

なお、各バージョンの検証は、変更&保存を2~3回程度繰り返して判定した。
正常に動作しなかったとしたバージョンでも、稀に成功するケースが観測されることがあり、厳密には確率的な不安定さがある可能性がある。（詳細は未検証）

## Suspected Cause

検証で想像できる原因は以下

1. 3.5.0のなんらかの変更の副作用で、元々不安定なauto-reloadが死んだ？->Auto-reloadはたびたび不具合が発生している（[例えば](https://youtrack.jetbrains.com/projects/KTOR/issues/KTOR-8821/Autoreloading-module-function-refs-not-working-since-3.2.0)）
2. kotlincが吐き出す.classファイルの中身が不正で、前回の成功状態を返している？ -> ホットリロード時に.classファイルのタイムスタンプおよび中身が更新されているため違いそう、そもそも「BUILD SUCCESSFUL」は表示されている
3. 2の検証のために、タイムスタンプや中身の確認を行ったが、その確認プロセスを行うと正常にホットリロードが動作した->レースコンディションの問題か？[これ](https://github.com/ktorio/ktor/issues/4717)に似ている。あるいは、確認によってDocker特有のファイルキャッシュの不整合が解消されるとか？
4. サーバへのリクエストが反映処理の起動を行えていない、トリガーが動作していない？->3.5.0で修正が入った[call event loop・worker event loopのPR](https://youtrack.jetbrains.com/projects/KTOR/issues/KTOR-9542/Netty-The-request-handler-runs-on-worker-event-loop-instead-of-call-event-loop-since-3.4.3)の副作用などの可能性はないだろうかとかが関係してないだろうか。

## Environment

OS: MacOS
VSCode: 1.125.0
Docker Client: 27.4.0
Docker Server （Engine）: 27.4.0
Java: 21
Kotlin: 2.4.0
Gradle: 9.5.1
Ktor: 3.5.0

## Additional Context

Apologies for any unclear parts due to machine translation.

Please let me know if you have any other questions or need any additional information.
I'll get back to you promptly.

Also, I can submit pull requests within my capabilities.
Considering the guidelines, what kind of changes should I commit?

I'm looking forward to the future development of this project. Thank you.
