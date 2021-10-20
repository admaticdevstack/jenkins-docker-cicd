# [Managing infrastructure as code with Terraform, Jenkins, and GitOps](https://cloud.google.com/architecture/managing-infrastructure-as-code-with-terraform-jenkins-and-gitops)

## Install Terraform

```bash
{
    sudo apt update
    sudo apt install wget unzip -y

    wget https://dl.dropbox.com/s/w8y89vemfylo20c/terraform_1.0.4_linux_amd64.zip
    unzip terraform_1.0.4_linux_amd64.zip

    sudo mv terraform /usr/bin
    rm terraform_1.0.4_linux_amd64.zip
}
```

## Install Jenkins

```bash
{
    sudo apt update
    sudo apt install openjdk-11-jre -y

    java -version
}
```

```output
...

openjdk version "11.0.11" 2021-04-20
OpenJDK Runtime Environment (build 11.0.11+9-Ubuntu-0ubuntu2.20.04)
OpenJDK 64-Bit Server VM (build 11.0.11+9-Ubuntu-0ubuntu2.20.04, mixed mode, sharing)
```

```bash
{
    wget https://get.jenkins.io/war-stable/2.289.3/jenkins.war
    java -jar jenkins.war --httpPort=8080
}
```

```output
--2021-08-25 12:45:56--  https://get.jenkins.io/war-stable/2.289.3/jenkins.war
Resolving get.jenkins.io (get.jenkins.io)... 52.167.253.43
Connecting to get.jenkins.io (get.jenkins.io)|52.167.253.43|:443... connected.
HTTP request sent, awaiting response... 302 Found
Location: https://mirror.xmission.com/jenkins/war-stable/2.289.3/jenkins.war [following]
--2021-08-25 12:45:57--  https://mirror.xmission.com/jenkins/war-stable/2.289.3/jenkins.war
Resolving mirror.xmission.com (mirror.xmission.com)... 198.60.22.13, 2607:fa18:0:3::13
Connecting to mirror.xmission.com (mirror.xmission.com)|198.60.22.13|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 74258876 (71M) [application/java-archive]
Saving to: ‘jenkins.war’

jenkins.war                                                                     100%[=====================================================================================================================================================================================================>]  70.82M  13.4MB/s    in 5.3s

2021-08-25 12:46:02 (13.4 MB/s) - ‘jenkins.war’ saved [74258876/74258876]

Running from: /home/admatic/jenkins.war
webroot: $user.home/.jenkins
2021-08-25 12:46:03.573+0000 [id=1]     INFO    org.eclipse.jetty.util.log.Log#initialized: Logging initialized @909ms to org.eclipse.jetty.util.log.JavaUtilLog
2021-08-25 12:46:03.714+0000 [id=1]     INFO    winstone.Logger#logInternal: Beginning extraction from war file
2021-08-25 12:46:05.019+0000 [id=1]     WARNING o.e.j.s.handler.ContextHandler#setContextPath: Empty contextPath
2021-08-25 12:46:05.106+0000 [id=1]     INFO    org.eclipse.jetty.server.Server#doStart: jetty-9.4.41.v20210516; built: 2021-05-16T23:56:28.993Z; git: 98607f93c7833e7dc59489b13f3cb0a114fb9f4c; jvm 11.0.11+9-Ubuntu-0ubuntu2.20.04
2021-08-25 12:46:05.548+0000 [id=1]     INFO    o.e.j.w.StandardDescriptorProcessor#visitServlet: NO JSP Support for /, did not find org.eclipse.jetty.jsp.JettyJspServlet
2021-08-25 12:46:05.617+0000 [id=1]     INFO    o.e.j.s.s.DefaultSessionIdManager#doStart: DefaultSessionIdManager workerName=node0
2021-08-25 12:46:05.618+0000 [id=1]     INFO    o.e.j.s.s.DefaultSessionIdManager#doStart: No SessionScavenger set, using defaults
2021-08-25 12:46:05.620+0000 [id=1]     INFO    o.e.j.server.session.HouseKeeper#startScavenging: node0 Scavenging every 600000ms
2021-08-25 12:46:06.368+0000 [id=1]     INFO    hudson.WebAppMain#contextInitialized: Jenkins home directory: /home/admatic/.jenkins found at: $user.home/.jenkins
2021-08-25 12:46:06.746+0000 [id=1]     INFO    o.e.j.s.handler.ContextHandler#doStart: Started w.@9fec931{Jenkins v2.289.3,/,file:///home/admatic/.jenkins/war/,AVAILABLE}{/home/admatic/.jenkins/war}
2021-08-25 12:46:06.817+0000 [id=1]     INFO    o.e.j.server.AbstractConnector#doStart: Started ServerConnector@2c78d320{HTTP/1.1, (http/1.1)}{0.0.0.0:8080}
2021-08-25 12:46:06.817+0000 [id=1]     INFO    org.eclipse.jetty.server.Server#doStart: Started @4155ms
2021-08-25 12:46:06.827+0000 [id=23]    INFO    winstone.Logger#logInternal: Winstone Servlet Engine running: controlPort=disabled
2021-08-25 12:46:07.334+0000 [id=30]    INFO    jenkins.InitReactorRunner$1#onAttained: Started initialization
2021-08-25 12:46:07.358+0000 [id=31]    INFO    jenkins.InitReactorRunner$1#onAttained: Listed all plugins
WARNING: An illegal reflective access operation has occurred
WARNING: Illegal reflective access by com.google.inject.internal.cglib.core.$ReflectUtils$2 (file:/home/admatic/.jenkins/war/WEB-INF/lib/guice-4.0.jar) to method java.lang.ClassLoader.defineClass(java.lang.String,byte[],int,int,java.security.ProtectionDomain)
WARNING: Please consider reporting this to the maintainers of com.google.inject.internal.cglib.core.$ReflectUtils$2
WARNING: Use --illegal-access=warn to enable warnings of further illegal reflective access operations
WARNING: All illegal access operations will be denied in a future release
2021-08-25 12:46:09.470+0000 [id=30]    INFO    jenkins.InitReactorRunner$1#onAttained: Prepared all plugins
2021-08-25 12:46:09.478+0000 [id=31]    INFO    jenkins.InitReactorRunner$1#onAttained: Started all plugins
2021-08-25 12:46:09.488+0000 [id=28]    INFO    jenkins.InitReactorRunner$1#onAttained: Augmented all extensions
2021-08-25 12:46:10.493+0000 [id=31]    INFO    jenkins.InitReactorRunner$1#onAttained: System config loaded
2021-08-25 12:46:10.495+0000 [id=31]    INFO    jenkins.InitReactorRunner$1#onAttained: System config adapted
2021-08-25 12:46:10.496+0000 [id=31]    INFO    jenkins.InitReactorRunner$1#onAttained: Loaded all jobs
2021-08-25 12:46:10.497+0000 [id=31]    INFO    jenkins.InitReactorRunner$1#onAttained: Configuration for all jobs updated
2021-08-25 12:46:10.562+0000 [id=44]    INFO    hudson.model.AsyncPeriodicWork#lambda$doRun$0: Started Download metadata
2021-08-25 12:46:10.616+0000 [id=44]    INFO    hudson.util.Retrier#start: Attempt #1 to do the action check updates server
2021-08-25 12:46:11.356+0000 [id=31]    INFO    jenkins.install.SetupWizard#init:

*************************************************************
*************************************************************
*************************************************************

Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

1c07f74953cd4b5eacf173e54d903705

This may also be found at: /home/admatic/.jenkins/secrets/initialAdminPassword

*************************************************************
*************************************************************
*************************************************************
```

Go to <http://localhost:8080>

![](images/0.png)

![](images/1.png)

![](images/2.png)

![](images/3.png)

![](images/4.png)

![](images/5.png)

![](images/6.png)

![](images/7.png)

![](images/8.png)

![](images/9.png)

![](images/10.png)

![](images/11.png)

![](images/12.png)

![](images/13.png)

![](images/14.png)

![](images/15.png)

![](images/16.png)

![](images/17.png)

![](images/18.png)

![](images/19.png)

![](images/20.png)

![](images/21.png)

![](images/22.png)

![](images/23.png)

![](images/24.png)

![](images/25.png)

![](images/26.png)

![](images/27.png)

![](images/28.png)

![](images/29.png)

![](images/30.png)

![](images/31.png)

![](images/32.png)

![](images/33.png)

![](images/34.png)

![](images/35.png)

![](images/36.png)

![](images/37.png)

![](images/38.png)

![](images/39.png)

![](images/40.png)

![](images/41.png)

![](images/42.png)
