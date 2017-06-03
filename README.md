# xq-nexus
Simple server for local repository

Fetch the new docker image from [docker hub](https://hub.docker.com/r/sonatype/nexus3/)

```sh
$> docker pull sonatype/nexus3
```

# Config & Launch nexus

```sh
$> mkdir /Volumes/Data/nexus-data && chmod a+w /Volumes/Data/nexus-data && chown -R 200 /Volumes/Data/nexus-data
$> docker run -d -p 5000:8081 --name nexus -v /Volumes/Data/nexus-data:/nexus-data sonatype/nexus3
```

# Nexus for maven repository

## Using custom repository for gradle project.

```
repositories {
    maven {
        url 'http://localhost:5000/repository/maven-central/'
    }
}

dependencies {
    testCompile group: 'junit', name: 'junit', version: '4.12'
    compile group: 'org.springframework.boot', name: 'spring-boot-starter-web', version: '1.5.3.RELEASE'
}
```

## Using custom repository for mvn project.

```xml
<profile>
    <id>custom-maven-center</id>
    <repositories>
        <repository>
            <id>custom-mvn-center</id>
            <name>Custom Maven Center</name>
            <releases>
                <enabled>true</enabled>
                <updatePolicy>always</updatePolicy>
                <checksumPolicy>warn</checksumPolicy>
            </releases>
            <snapshots>
                <enabled>false</enabled>
                <updatePolicy>never</updatePolicy>
                <checksumPolicy>fail</checksumPolicy>
            </snapshots>
            <url>http://localhost:5000/repository/maven-central/</url>
            <layout>default</layout>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>custom-mvn-center-plugin</id>
            <name>Custom Maven Center Plugin</name>
            <releases>
                <enabled>true</enabled>
                <updatePolicy>always</updatePolicy>
                <checksumPolicy>warn</checksumPolicy>
            </releases>
            <snapshots>
                <enabled>false</enabled>
                <updatePolicy>never</updatePolicy>
                <checksumPolicy>fail</checksumPolicy>
            </snapshots>
            <url>http://localhost:5000/repository/maven-central/</url>
            <layout>default</layout>
        </pluginRepository>
    </pluginRepositories>
</profile>
```
