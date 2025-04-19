

Tomcat servers can be identified by the Server header in the HTTP response. If the server is operating behind a reverse proxy, requesting an invalid page should reveal the server and version. Here we can see that Tomcat version `9.0.30` is in use.

http://app-dev.inlanefreight.local:8080/invalid

```shell-session
curl -s http://app-dev.inlanefreight.local:8080/docs/ | grep Tomcat
```

Custom error pages may be in use that do not leak this version information. In this case, another method of detecting a Tomcat server and version is through the `/docs` page.


The `bin` folder stores scripts and binaries needed to start and run a Tomcat server. The `conf` folder stores various configuration files used by Tomcat. The `tomcat-users.xml` file stores user credentials and their assigned roles. The `lib` folder holds the various JAR files needed for the correct functioning of Tomcat. The `logs` and `temp` folders store temporary log files. The `webapps` folder is the default webroot of Tomcat and hosts all the applications. The `work` folder acts as a cache and is used to store data during runtime.

```shell-session
├── bin
├── conf
│   ├── catalina.policy
│   ├── catalina.properties
│   ├── context.xml
│   ├── tomcat-users.xml
│   ├── tomcat-users.xsd
│   └── web.xml
├── lib
├── logs
├── temp
├── webapps
│   ├── manager
│   │   ├── images
│   │   ├── META-INF
│   │   └── WEB-INF
|   |       └── web.xml
│   └── ROOT
│       └── WEB-INF
└── work
    └── Catalina
        └── localhost
```

The most important file among these is `WEB-INF/web.xml`, which is known as the deployment descriptor. This file stores information about the routes used by the application and the classes handling these routes. All compiled classes used by the application should be stored in the `WEB-INF/classes` folder. These classes might contain important business logic as well as sensitive information.


After fingerprinting the Tomcat instance, unless it has a known vulnerability, we'll typically want to look for the `/manager` and the `/host-manager` pages.
