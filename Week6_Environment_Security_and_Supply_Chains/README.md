# **Week 6**

### Grading

Task #|Points|Description|
-----|:---:|----------|
Task 1 | 1 | Secure Running Environment
Task 2 | 1 | Supply Chain Attacks 
Task 3 | 2 | Securing docker

---

# Tasks

### Task 1: Secure Running Environment?

Virtualization

-Virtualization creates isolated environment from the host and does not compromise whole system if it gets contaminated. This also means that sensitive programs or databases can be isolated to more secure virtual machines, while not so sensitive information can be kept in less secured machine. Test environments can be highly valuable aswell as potential possibility to snapshot and rollback. Test environment itself creates possibility to create replica of the system and test it against potential threats without breaking the actual system. While snapshotting and rollbacking ensures that user is always able to go back and start all over again. Virtualization gives better tools to monitor and audit usage of VMs. However Virtualization is not completly flawless. There are cases called VM escape, when the attack has been able to access the host through Virtual Machine. Also Inter-VM attacks have become more common, this happens when attack has gotten access to one of the Virtual Machines and then launches attack through compromised machine against other VMs. Patching VM can also cause problems when it might require more effort, which causes some VMs not to be upgraded whenever necessary and lead to potential vulnerabilities.

https://learn.microsoft.com/en-us/windows-hardware/design/device-experiences/oem-vbs
https://ieeexplore.ieee.org/document/9900211
https://en.wikipedia.org/wiki/Virtual_machine_escape
https://people.cs.ksu.edu/~zhangs84/papers/cloudTR.pdf

Container

-Container is a lightweight, standalone and executable software package. This package includes everything required to run certain software. Containers are isolated from other containers and from the host. Containers in general offer both development and security benefits. Isolation provides layer of a security, compromising one of the containers does not necessarely compromise rest of the containers or the host. Consistency brings development team on the same page, reducing machine specific problems. Containers are immune to changes, onces container is build it can't be changed and requires a new instance to be build if any changes are applied. Containers however do have multiple threats. If the image has vulnerable components whole container can be exploited. Runtime threats are executed in order to gain for example root access to the system. Incorrectly configured containers might lead to security problems. If containers communicate with each other this might lead to security problems in api side. These issues can be mitigated by regularely updating containers and monitoring vulnerable components. Giving containers as little privaledges as possbile, configuring containers properly, keeping network policies updated. No old containers are left hanging instead once container is upgraded, automatically delete older version. Monitoring and logging activity of the container.

https://docs.docker.com/engine/security/
https://sysdig.com/blog/cisos-financial-services/
https://sysdig.com/content/c/pf-finserv-5-cloud-security-best-practices?x=u_WFRi


---

### Task 2: Supply Chain Attacks

In this task we are looking at the difficulties handling supply chain attacks, specifically detecting and responding.

For this scenario you are working for a networking hardware and software company, and you're tasked with securing their supply chain. The company manufactures and sells routers with their own software and other various networking accessories B2B and B2C.  Some parts for the routers have to be outsourced and manufactured outside company.

Research and write a report on concrete actions you could implement on the supply chain, trying to make sure the product is not being tampered or researched with malicious intent. Keep in mind, that the supply chain includes third party tools, code and update providing, as well as other companies maintaining firmware. Your supply chain must include **at least four** actors including your company. You should analyze the points of concerns in the report.

Provide reasoning for your choices and analyze what potential problems and additional actions these choices might require from your company.

Probable actors in such supply chains include, but are not limited to:

- Employees, in-house and outsourced
- Transportation companies
- Retail companies
- Storage facilities
- Part suppliers

Hardware

Software


<details>
<summary>Example supply chain</summary>
<br>

Hardware
- 3rd party company X manufactures antennas for the routers
- Truck company Y transports them to 
- Factory Z, where it is assembled by workers 
- Y transports them to resellers A and B

<br>

Software
- Own employees create it
- Company C provides contractual coders for help
- Company D audits software
- Company E hosts internal tools

<br>
You can use the examply supply chain in your task if you want to.
<br>
</details>

Some concepts to help you get started:
- NDR (Network Detection and Response)
- UBA (User Behavioral Analytics)
- EDR (Endpoint Detection and Response)
- TPM (Trusted Platform Module)

Real-life cases for inspiration:
- [SolarWinds](https://www.gao.gov/blog/solarwinds-cyberattack-demands-significant-federal-and-private-sector-response-infographic)
- [Routers, servers and networking equipment from the USA](https://www.infoworld.com/article/2608141/snowden--the-nsa-planted-backdoors-in-cisco-products.html) | Notice the second page accessible at the bottom of the article

**Minimum 500 words,  
Maximum 4 visual representations,  
Each visual representation is minus 50 words off the total required.**

For example a report with 3 visuals requires 350 words.  
The visuals must be useful for the raport, ex. company logos do not count.


Brief summary of the company:

Company provides digital communications technology services to international clients all over the world.

Company provides VoIP services, cloud-based system for communication. Company has desktop version supporting windows, linux, mac, iphone and android. In addtion to that company sells Android based devices for confrence rooms which uses specific company software.

Hardware:
    Company's device is based on heavily modified Android. Upgrades are done through cloud. Device itself is built by outsourced company in China and all of the hardware is made by multiple companies specialising to the elements.
        List of components:
            Microphone, Provided by company X
            Speaker, Provided by company X
            Display, Provided by company Y
            Networking components, Provided by company Z
            Battery, Provided by company F
            Camera, Provided by company X

Software:
    Company App, Created by the company
    Modified Android OS, Created by the company
    Device drivers, provided by each company doing specific component.
    Connectivity Software, Created by the company
    Audio & video codecs, provided by company X

Actors in a supply-chain.

- Employees, in-house and outsourced
    -in-house: Employees do have access to company IP, such as design and source code.
    -Outsorced: Only factory assembling the device has access to all of the components. Software is installed by in-house employees
- Transportation companies
    -Each component provider transports components directly to manufactor.
- Storage facilities
    -Storage facilities aswell are provided by manufactor.
- Part suppliers
    -Part suppliers are responsible of providing required components directly to manufactor.

Company is constantly monitoring traffic on their servers using NDR system. System detects threats and reports them directly to company.

---

### Task 3: Securing Docker

**Linux required for full completion; [Course provided VM](https://ouspg.org/resources/laboratories/)**

In this exercise we are checking out some tools and practices to help you create better and more secure Docker containers. You are to either use your own Dockerfiles or images, create your own dockerfile for this exercise or you can use ones created by other people. The important part here is auditing and fixing the files, image or container. You shouldn't use ones that have been well audited; the files you choose for this task should provide some output, this is likely with most files.

These tasks provide a great chance to contribute to open source projects, especially if you are looking for a great way to make your first pull requests. You can find Open Source Software with Dockerfiles and lint these, fix the problems provided by the linter when valid, open up a pull request and suggest these fixes with good explanations. 

Your analysis with Trivy (or scanner of your choice) can be opened as an issue, or you can write it into a report and try to open a pull request for it or fixes you made. These might require more work to get accepted though, but can be a great contribution to certain projects.

> A small warning, as some of these tools can be quite complicated, reading through the documentation could take some time. All necessary parts **should** be in this task sheet, but not all problems can be covered. And due to the nature of the course, we expect students to be able to read and take in documentations.

---

### Task 3A) Linting the Dockerfile 0.5p

We will start by first linting the Dockerfile, this will let you know of problems with the configuration, for example using the ```:latest``` tag. These tools will guide you towards  the best practices regarding [Dockerfiles](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/). 

You are free to use any Dockerfile linting tool you want, however a great tool worthy of a recommendation is [Hadolint](https://github.com/hadolint/hadolint), they have the tool packaged into a container and they also have a [GUI Web tool](https://hadolint.github.io/hadolint/) for those interested. The web tool is quite great, but doesn't offer the same customizability as the CLI tool, the functionality is enough for this task, especially if you don't feel comfortable on the command line. As stated, the tool can also be run on Docker, this makes it easier to run on different environments. 

```docker pull hadolint/hadolint```  
To pull the image and can be run with:  
```docker run --rm -i hadolint/hadolint < Dockerfile```

> For running with custom rules and/or personal modifications you should refer to their own [instructions](https://github.com/hadolint/hadolint#how-to-use). 

Depending on the type of Dockerfile you are linting and which tool you are using to do this, you will be presented either with just the problems or the tool can give you directions on fixing these issues. 

Not all problems indicated by the tool have to be fixed, and not all warnings should be fixed blindly, but of course you should aim for fixing everything you can, while not breaking the program.

### What to return:
- What linter you used
- The dockerfile, before and after fixes
- Screenshot **or** .md file of the linter before and after fixes

[Hadolint](https://github.com/hadolint/hadolint)  
[Hadolint Web GUI](https://hadolint.github.io/hadolint/) 

---

### Task 3B) Container Image Analysis 0.5p

Next comes analyzing the image for vulnerabilities in containers. It is also common to use these scanners in CI/CD pipelines. Again, you can use any analyzer you want, but we're going to recommend [Trivy](https://github.com/aquasecurity/trivy). Trivy is an open source project by [Aquasecurity](https://www.aquasec.com/), and it has quite the nice [documentation](https://aquasecurity.github.io/trivy/v0.41/). This task should be doable without reading too much documentation, we do  however recommend checking it out.  They cover at least **most common** use cases and problems there. You can also refer to this documentation if you want to know more about the tool itself and other ways you can use it, such as Kubernetes, filesystem and GitHub repository scanning.

Trivy can be run on docker with  
```docker run aquasec/trivy image <image_name>```  
Or it can be installed from a [binary](https://github.com/aquasecurity/trivy/releases/tag/v0.45.1) or from a [package manager](https://aquasecurity.github.io/trivy/v0.45/getting-started/installation/)  
And then you can run it with:  
```trivy image <image_name>``` for Docker images.  
  
Here you should **try** to fix atleast some errors, the recommended tool Trivy can tell you if a vulnerable piece of software has a patch or a newer version that addressed the vulnerability. However we do understand that not every vulnerability can be fixed.

### What to return:
- What analyzer you used
- The image used, **or** the Dockerfile to build it
- Screenshot **or** .md file of the analyzer output before and after the fixes

[Trivy](https://github.com/aquasecurity/trivy)  
[Trivy docs](https://aquasecurity.github.io/trivy/v0.41/)

---

### Task 3C) Runtime Security 1p

Finally we are going to look at the runtime security of containers, here again you can use any tool you want to, but we're going to recommend a tool originally by [Sysdig](https://sysdig.com/), currently under [CNCF](https://www.cncf.io/). The tool [Falco](https://github.com/falcosecurity/falco) is designed to detect and alert in real-time. The tool is for Linux operating systems.

They as well have a vast and very detailed [documentation](https://falco.org/docs/) with multiple ways to install and run the tool. The documentation has instructions for [installing on different Linux distributions](https://falco.org/docs/getting-started/source/), and we recommend following either these, or installing the [falco binary](https://falco.org/docs/getting-started/installation/#falco-binary). You can also use their own [tutorials](https://falco.org/docs/tutorials/) to get more familiar with the tool.

### Triggering Alerts

Your goal here is to choose the rules, start the tool and trigger alerts about and from within the containers. One easy way you can trigger an alert is with ```--privileged``` containers, as the ```--privileged``` flag itself creates an alert.  

However you are to trigger another alert from within the containers, here again their documentation provides great instructions on which types of activities create which types of alerts, and with which rulesets.

> `docker run -it <image_name> sh` can be used to start an interactive shell in a container. You can use any shell you want, like bash, but not every distribution, or container has it.

You can modify the rules provided with the installation, most likely not necessary, however it is encouraged to take look at least.

### What to return:
- What runtime security scanner you used
- The image used, **or** the Dockerfile to build it
- Screenshot **or** .md file of the alerts created
- What commands and/or activities used to trigger the alerts

[Falco](https://github.com/falcosecurity/falco)  
[Falco docs](https://falco.org/docs/)
