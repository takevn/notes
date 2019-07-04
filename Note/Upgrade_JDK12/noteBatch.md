Batch
# dsp-batchのディレクトリで、
```
./gradlew clean fatJar
```

javacompiler
target byte code versions
1.8 -> 12


File: build.Gradle

//apply plugin: 'java'
//apply plugin: 'eu.appsatori.fatjar'


buildscript {
    repositories {
        jcenter()
        mavenCentral()
    }
    dependencies {
        classpath "eu.appsatori:gradle-fatjar-plugin:0.3"

    }
}

plugins {
    id "io.franzbecker.gradle-lombok" version "3.0.0" // latest 20190521
    id "com.intershop.gradle.jaxb" version "3.0.3"
//    id "com.github.johnrengelman.shadow" version "5.0.0"


}


//sourceCompatibility = 12



apply plugin: 'java'
//// todo comment below
apply plugin: 'eu.appsatori.fatjar'


repositories {
    jcenter()
}

//sourceCompatibility = 12
// In this section you declare the dependencies for your production and test code
dependencies {

    compile group: 'org.mariadb.jdbc', name: 'mariadb-java-client', version: '2.2.6'

    //Google OAuth2 API Client Library for Java
    //compile 'com.google.apis:google-api-services-oauth2:v1-rev144-1.24.1'
    compile group: 'com.google.auth', name: 'google-auth-library-oauth2-http', version: '0.10.0'


    //Google big query api
    // https://mvnrepository.com/artifact/com.google.cloud/google-cloud-bigquery
    compile group: 'com.google.cloud', name: 'google-cloud-bigquery', version: '1.48.0'

    // slf4j
    // https://mvnrepository.com/artifact/org.slf4j/slf4j-api
    compile group: 'org.slf4j', name: 'slf4j-api', version: '1.7.25'
    def logbackVersion = '1.2.3'
    compile("ch.qos.logback:logback-classic:${logbackVersion}")

    compile group: 'com.google.guava', name: 'guava', version: '22.0'

    // jackson
    def jacksonVersion = '2.0.0'
    compile "com.fasterxml.jackson.core:jackson-databind:${jacksonVersion}"
    compile "com.fasterxml.jackson.core:jackson-core:${jacksonVersion}"
    compile "com.fasterxml.jackson.core:jackson-annotations:${jacksonVersion}"
//    compile group: 'com.fasterxml.jackson.core', name: 'jackson-databind', version: '2.9.9'
//    compile group: 'com.fasterxml.jackson.core', name: 'jackson-core', version: '2.9.9'
//    compile group: 'com.fasterxml.jackson.core', name: 'jackson-annotations', version: '2.9.9'

    compileOnly group: 'org.projectlombok', name: 'lombok', version: '1.16.18'
    compileOnly group: 'org.projectlombok', name: 'lombok', version: '1.18.8'
//    compileOnly 'org.projectlombok:lombok:1.18.6'
//    annotationProcessor 'org.projectlombok:lombok:1.18.6'
//    testCompileOnly group: 'org.projectlombok', name: 'lombok', version: '1.16.18'

    // lz4
    // https://mvnrepository.com/artifact/net.jpountz.lz4/lz4z
    compile group: 'net.jpountz.lz4', name: 'lz4', version: '1.3.0'


    // commons lang3
    // https://mvnrepository.com/artifact/org.apache.commons/commons-lang3
    compile group: 'org.apache.commons', name: 'commons-lang3', version: '3.5'
    compile group: 'org.apache.commons', name: 'commons-csv', version: '1.6'

    // couchbase java sdk
    // https://mvnrepository.com/artifact/com.couchbase.client/java-client
//    compile group: 'com.couchbase.client', name: 'java-client', version: '2.4.6'
    compile group: 'com.couchbase.client', name: 'java-client', version: '2.7.6'


    // aerospike client sdk
    compile group: 'com.aerospike', name: 'aerospike-client', version: '4.1.2'

    // commons codec
    // https://mvnrepository.com/artifact/commons-codec/commons-codec
    compile group: 'commons-codec', name: 'commons-codec', version: '1.10'

    // JCommander
    // http://jcommander.org/#_download
    compile "com.beust:jcommander:1.71"

    // https://mvnrepository.com/artifact/javax.xml.bind/jaxb-api
    compile group: 'javax.xml.bind', name: 'jaxb-api', version: '2.3.1'
    // https://mvnrepository.com/artifact/com.sun.xml.bind/jaxb-core
    compile group: 'com.sun.xml.bind', name: 'jaxb-core', version: '2.3.0.1'
    // https://mvnrepository.com/artifact/com.sun.xml.bind/jaxb-impl
    compile group: 'com.sun.xml.bind', name: 'jaxb-impl', version: '2.3.2'
//
//    compile group: 'org.eclipse.persistence', name: 'org.eclipse.persistence.moxy', version: '2.7.4'

//    compile group: 'org.eclipse.persistence', name: 'org.eclipse.persistence.moxy', version: '2.7.3'
    // 2.2.x version
//    implementation "javax.xml.bind:jaxb-api:2.2.11"
//    implementation "com.sun.xml.bind:jaxb-core:2.2.11"
//    implementation "com.sun.xml.bind:jaxb-impl:2.2.11"
//    implementation "javax.activation:activation:1.1.1"

//    implementation "javax.xml.bind:jaxb-api:2.3.1"
    // https://mvnrepository.com/artifact/org.glassfish.jaxb/jaxb-runtime
//    compile group: 'org.glassfish.jaxb', name: 'jaxb-runtime', version: '2.3.2'



    // Exception in thread "main" java.lang.NoClassDefFoundError: javax/xml/bind/JAXBException
//    implementation "javax.activation:activation:1.1.1"


    // junit
// https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api
    testCompile group: 'org.junit.jupiter', name: 'junit-jupiter-api', version: '5.3.0'
    // https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-engine
    testCompile group: 'org.junit.jupiter', name: 'junit-jupiter-engine', version: '5.3.0'
    // https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-params
    testCompile group: 'org.junit.jupiter', name: 'junit-jupiter-params', version: '5.3.0'
    // https://mvnrepository.com/artifact/org.junit.vintage/junit-vintage-engine
    testRuntime group: 'org.junit.vintage', name: 'junit-vintage-engine', version: '5.3.0'
    // https://mvnrepository.com/artifact/org.junit.platform/junit-platform-console-standalone
    testRuntime group: 'org.junit.platform', name: 'junit-platform-console-standalone', version: '1.3.0'
    // https://mvnrepository.com/artifact/org.junit.platform/junit-platform-runner
    testCompile group: 'org.junit.platform', name: 'junit-platform-runner', version: '1.3.0'
    // https://mvnrepository.com/artifact/org.junit.platform/junit-platform-launcher
    testRuntime group: 'org.junit.platform', name: 'junit-platform-launcher', version: '1.3.0'
}

//jar {
//    manifest {
//        attributes "Main-Class" : "app.Main"
//        attributes 'version': "1.0"
//    }
//}
//
//shadowJar {
////    mergeServiceFiles('META-INF/spring.*')
////    exclude "META-INF/*.SF"
////    exclude "META-INF/*.DSA"
////    exclude "META-INF/*.RSA"
////    exclude "META-INF/LICENSE"
////    archiveName = 'dsp-batch.jar'
//    archiveFileName = 'dsp-batch.jar'
//    baseName = 'monitor'
//    appendix = 'bin'
//    version = "1.0"
//
//}
