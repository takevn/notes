update　JDK　１２
米Oracleは3月19日、「Java SE 12（JDK 12）」を公開した。
@noda-takahiro さん
JDKアップデート（ver.12)のタスクなんですが、
https://gmo-am.atlassian.net/browse/RM-440

# 事前準備
localのDockerを起動し、
リクエストを送って、valid=1のレスポンスが返ってくることを確認する。

->答え：2通りあります。

1. commandでcurlを使う
curl -v -H "Content-Type: application/json" -X POST "localhost/dsp/bid/v1?ssp_id=1" --data @sampledata/bidsample/bidtrial/sample-gmossp-real_phase8.json
curl -v -H "Content-Type: application/json" -X POST "localhost/dsp/bid/v1?ssp_id=1" --data @sampledata/bidsample/sample-gmossp.json

2. テストクラスからリクエストを送る
BidApiGmoSspDockerTest#doPost_GMO_SSP_phase8

**Dockerを起動した後しばらく待ちないと"valid":1が出ない。！！！**

STG:
http://mon.st.dsp.reemo-ad.jp/debug/kvs/v1?key=uyVlTvzCfYwwBDHy&namespace=USER_DATA

mon.st.dsp.reemo-ad.jp:80

DEVELOPMENT:
http://localhost/dsp/debug/kvs/v1?key=uyVlTvzCfYwwBDHy&namespace=USER_DATA


# export JAVA_HOME=`ディレクトリ`
参考リンク: https://qiita.com/Terry3/items/9a1a8f1b6de349cee5ef
https://stackoverflow.com/questions/52524112/how-do-i-install-java-on-mac-osx-allowing-version-switching
export JAVA_8_HOME=$(/usr/libexec/java_home -v1.8)
export JAVA_HOME=`/usr/libexec/java_home -v 10.0.2`
JAVA12
export JAVA_HOME=`/usr/libexec/java_home -v 12.0.1`
or
export JAVA_HOME=`/usr/libexec/java_home -v 12`
or
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-12.jdk/Contents/Home
# confirm JAVA_HOME
echo $JAVA_HOME
/usr/libexec/java_home
/usr/libexec/java_home -V
# Remove jdk
sudo rm -rf jdk1.7.0_71.jdk

/System/Library/Frameworks/JavaVM.framework/Versions/A/Commands/java_home
/Library/Java/JavaVirtualMachines/jdk-12.0.1.jdk/Contents/Home

# To define a JDK and a mobile SDK in IntelliJ IDEA #
https://www.jetbrains.com/help/idea/configuring-mobile-java-sdk.html
1. Open the Project Structure dialog (e.g. ⌘;).
2. In the leftmost pane, under Platform Settings, click SDKs.
3. Above the pane to the right, click icons general add svg and select JDK.

# Jetty Versions
最新版：9.4.18.v20190429/  
https://repo1.maven.org/maven2/org/eclipse/jetty/jetty-distribution/

# unable-to-use-intellij-with-a-generated-sources-folder MomentumResponseExt, openrtb
Fix build.gradle de nhan nhung file import jp.gmoam.openrtb.momentum.response.MomentumResponseExt;
https://stackoverflow.com/questions/5170620/unable-to-use-intellij-with-a-generated-sources-folder
edit
sourceSets {
    main {
        proto {
            // In addition to the default 'src/main/proto'
//            srcDir 'src/main/proto'
//            srcDir 'src/main/proto-gen'


# install protobuf
brew install protobuf

# upgradle gradle
./gradlew wrapper --gradle-version 2.12
./gradlew wrapper --gradle-version=5.4.1
edit file: gradle/wrapper/gradle-wrapper.properties
distributionUrl=https\://services.gradle.org/distributions/gradle-2.10-all.zip

gradle --version

#  https://docs.gradle.org/5.4.1/release-notes.html
./gradlew updateJettyWebapp

Welcome to Gradle 5.4.1!

Here are the highlights of this release:
 - Run builds with JDK12

# SDK to change gradle version
 sdk install gradle
Or to install a specific version:

sdk install gradle 2.2
Or use to use a specific installed version:

sdk use gradle 2.2
To see which versions are installed and available:

sdk list gradle

# Could not determine java version from '12.0.1'.
As distributionUrl is still pointing to older version, upgrade wrapper using:

gradle wrapper --gradle-version 5.4.1
Note: Use gradle and not gradlew

sdk use gradle 5.4.1

#  Could not get file details of /Users/usr0102983/projects/dsp-monitor/gradle/wrapper/gradle-wrapper.jar: permission denied
chmod +x ./gradle

~/projects/dsp-monitor  master ✗ 2.4.1                                                           8d ⚑ ◒  ⍉
▶ ./gradlew clean fatJar --stacktrace
# Caused by: groovy.lang.MissingPropertyException: Could not get unknown property 'classesDir' for main classes of type org.gradle.api.internal.tasks.DefaultSourceSetOutput.
SourceSetOutput.getClassesDir() was deprecated in Gradle 4 and removed in Gradle 5. Please use getClassesDirs() in Gradle 5

->
# fatJar -> shadow
https://qiita.com/kmdsbng/items/ab093146a62afa34b739
```
Configures the shadowJar task to exclude any JAR index or cryptographic signature files matching the following patterns:
META-INF/INDEX.LIST
META-INF/*.SF
META-INF/*.DSA
META-INF/*.RSA
```

plugins {
    id "com.github.johnrengelman.shadow" version "5.0.0"
}
jar {
    manifest {
        attributes "Main-Class" : "app.Main"
        attributes 'version': projectVersion
    }
}

./gradlew shadowJar

# Lombok
Lombok supports Java 12 since Early Access version of Java 12.
https://github.com/rzwitserloot/lombok/issues/1888
Use the latest available versions of Lombok library (1.18.6+), Lombok IDE plugin (0.24+) and IntelliJ IDEA itself (2019.1+). Don't forget to 'Enable Annotation Processing' within IntelliJ's settings.

build.gradle

plugins {
    id 'java-library'
}

repositories {
    mavenCentral()
}

dependencies {
    compileOnly 'org.projectlombok:lombok:1.18.6'
    annotationProcessor 'org.projectlombok:lombok:1.18.6'
}
# yaml
https://mvnrepository.com/artifact/org.yaml/snakeyaml/1.24

# Error:java: リリース・バージョン12はサポートされていません

# Docker
dsp_monitor
dsp_deliver
dsp_aerospike
はdocker rmi実行しました。

# What is the difference between declaring repositories in the buildScript section of the gradle build or in the root level of the build.
The repositories in the buildScript block are used to fetch the dependencies of your buildScript dependencies. These are the dependencies that are put on the classpath of your build and that you can refer to from your build file. For instance extra plugins that exist on the internet.

The repositories on the root level are used to fetch the dependencies that your project depends on. So all the dependencies you need to compile your project.

# jackson -> có bản update mới nhưng thực ra không cần, vấn đề lúc load đuợc lúc không load đuợc chưa hiểu vì sao
// https://mvnrepository.com/artifact/com.fasterxml.jackson.core/
//    compile group: 'com.fasterxml.jackson.core', name: 'jackson-databind', version: '2.9.9'
//    compile group: 'com.fasterxml.jackson.core', name: 'jackson-core', version: '2.9.9'
//    compile group: 'com.fasterxml.jackson.core', name: 'jackson-annotations', version: '2.9.9'

# plugin java.
plugins {
    id 'java'
}
-> Not OK
apply plugin: 'java'
-> OK
* Why!!! 20190530
-> https://docs.gradle.org/4.10/userguide/java_plugin.html
# apply plugin vs plugins
* The plugins block is the newer method of applying plugins, and they must be available in the Gradle plugin repository.
 The apply approach is the older, yet more flexible method of adding a plugin to your build.

The new plugins method does not work in multi-project configurations (subprojects, allprojects),
but will work on the build configuration for each child project.

I would think that as functionality progresses, the plugins configuration method will overtake the older approach,
but at this point both can be and are used concurrently.


# Gradle
for core Gradle plugins or plugins already available to the build script

for binary Gradle plugins that need to be resolved

# Jetty configure
https://github.com/gmo-am/dsp-deliver/tree/develop/jettybase/lib/jnr

https://github.com/gmo-am/dsp-deliver/tree/develop/jettybase/start.d
更新が必要？
