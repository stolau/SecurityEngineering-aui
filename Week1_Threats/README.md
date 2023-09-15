# Week 1

# Tasks

### Task 1: What measures have you taken to protect yourself from cyber crimes?

Nothing much. Avoiding public Wi-Fi. Using password management tool, having automatically generated unique password in every application I'm using.

Before I started studying my pokerstar account information got stolen in massive dataleak. There were no information leak, until someone decided to use my account to play some money from another credit card. I could have been more aware of the leak, but having accounts with stolen logins not being frozen instantly until password is changed was most likely bigger issue.
---

### Task 2: Personal Threat Model


THREAT MODEL:


I currently do have 46 accounts in my Password Manager, which all of the contains unique password that was changed within last 6months.
Each site contains some personal information, such as name, address and credit card details. Most of the sites are also protected with 2-step verification. However I have noted some times not having proper way of implementing 2-step verification. e.g. Accounts can be logged in from a new computer and only mention is email of undetected login.
Authenticators are spread between multiple applications and even physical phones.

Likelyhood: 3
weak and repeated pwd: 0
Impact: 10
Mitigate: If password manager is compromised. Instantly abandoning password manager and start going login sites 1 by 1 changing password.

---

### Task 3: Company Security Policy

Company's Password Policy:

1. Overview
    Company is enforcing password policy for each employee. This password policy must be followed. If employee breaks given password policy, company can find employee accountable for damages caused.

2. Purpose
    Password policy establishes rules for employees to protect company's IP.

3. Policy

    A. GENERAL 

    Each employee should follow the company's password policy. Single password is used for access to all company related information.
    Company will force password change every 4 months. Employee is not allowed to share the password to anyone in the company, not even
    IT-support even if requested. If password is incorrectly leaked to another employee or got caught by phising attack. Employee is required
    instantly call the local IT-support and company account will be frozen until password is changed.

    Password needs to fill following criteria:
        - Minimum length 8 characters.
        - Maximum length 74 characters.
        - Password is not found from any public database of breached passwords.
        - Password should not contain more than 2 sequential characters
        - Password should not contain any repeated (Example 123)
        
    Recommended by NIST. Company is not enforcing special characters, upper case letters or numbers. But highly advice users to use them.
    Two-factor authentication is required with employee's company phone.

    Be aware of your surroundings all the times while inputing your password to any of company devices. Especially in public places.

    Company is allowing 4 failed attempts. After that your account will be temporarely suspended for 15 minutes. If process is repeated
    account will be frozen until IT-support has reset employee's password

    B. ENFORCEMENT

    Company employee found in policy violation can be held accountable for damages caused by his/her actions.

Physical Access Policy

1. Overview
    Each employee is required to follow company's physical access policy. Management and monitoring of physical access to company's properties is important to protect company's IP, devices and employee safety.

2. Purpose
    Physical Facility Access Policy establishes rules for employees with physical access to company's properties.

3. Policy
    A. GENERAL
    
    Physical access to company's properties is documented and managed. Properties are physically protected.

    Manager is responsible to grant access for a new employeer and managing proper access to current employees of the company.

    Access to certain parts of the company property is restricted if employee is not required to use the area.

    Access rights of each employee is required to be reviewed every 4 months. Employees who no longer need a specific access should removed.

    B. KEY ACCESS

    Each employee is given access key to local company area. By default access key contains access to common areas inside the company building.

    Employee is also granted access to specific job required areas.

    Lost access key must be reported immediately to local manager.

    Access key shall be removed once employee's contract is terminated.

    Access records are regularly reviewed by company.

    C. VISITOR ACCESS

    Local manager is required to grant visitors right to access to area. Visitor must be escorted by employee all the time.

    Visitors are logged to company's questbook.

    If visitor is given access key. Access key must be removed before visitor leaves company property.

    D. ENFORCEMENT

    Company employee found in policy violation can be held accountable for damages caused by his/her actions.


---

### Task 4: Security Audit

In the previous tasks we tried to map out our precious data and security of our machines. Now we can perform a couple of tests to see if we find any anomalies or unsecured data. We also deploy a Security Information and Event Management software to monitor and analyze systems.

### Task 4A: Network scan 

1. Did you find devices you did not know were in your network?
    no unknown open ports
    PORT     STATE SERVICE
        631/tcp  open  ipp
        8080/tcp open  http-proxy

2. Were there open ports which should have been closed?
    Basically http.server on 8080. using if for other purposes and it was left on
3. Did nmap find any vulnerabilities with the scripts?
    no
4. Screenshot of the topology of your network. You can redact device information if you want.


### Task 4B: Account Security

1. Has your account details leaked?
    Yes, 4 times. All of the leaks are almost 10years old.
2. Screenshot of haveibeenpwned search, you can redact information if you want.
    ![screenshot](https://github.com/ouspg/SecurityEngineering/blob/main/Week1_Threats/Images/pwned.png)

3. Did you change passwords and/or email + password combos, that were leaked, if not, do it.
    Yes, long time ago.

### Task 4C: [Wazuh](https://www.wazuh.com)

Wazuh is an free and open source "unified XDR and SIEM protection for endpoints and cloud workloads." In this task we are going to focus more on the [SIEM](https://www.gartner.com/en/information-technology/glossary/security-information-and-event-management-siem) side of things. Take a look at their [website](https://wazuh.com/platform/siem/) and [github](https://github.com/wazuh/wazuh) to familiarize yourself with the capabilities and features Wazuh SIEM offers.

>**Note**
>Task has been written on Version 4.5, when going through documentation, you can switch to Version 4.5 from the top-left.

Start of with deploying the Wazuh [single-node on Docker](https://documentation.wazuh.com/current/deployment-options/docker/wazuh-container.html). You should go through the documentation to understand what's going on, but the following commands should be enough:

```console
git clone https://github.com/wazuh/wazuh-docker.git -b v4.5.1
cd wazuh-docker/single-node
docker-compose -f generate-indexer-certs.yml run --rm generator
docker-compose up -d
```

You can access the Wazuh (WUI)WebUI at your localhost, to do this go to [https://localhost](https://localhost). By default Wazuh uses self signed certs and you won't be directed to the site directly, instead click the advanced tab and find the button for "Accept the risk and continue". This will direct you to the site, and from then on you should be able to use it normally.

Next deploy atleast 2 agents with different operating systems, one on a virtual machine and one on your own OS for example. You can do this via the Wazuh WUI(Web User Interface), or when your OS is not available there, you can follow [this](https://documentation.wazuh.com/current/user-manual/agent-enrollment/index.html), the first method is recommended. The IP address is your internal ip address. This step should be straightforward.

Create a directory named integrity and add a file to it on both machines and enable FIM(File Integrity Monitoring) on both agents, you should also set the scan frequency at around 60 seconds, so you won't have to wait for the events. 

You are to trigger the FIM with atleast two different events. Then answer the questions below.

**What to return:**
1. What rule descriptions did you get?
2. What are the MITRE ATT&CK techniques(include ID) Wazuh reports for these events?
3. What is the reported MITRE techniques for deleting files or directories inside monitored directories?
4. Explain in your own words where, when and why should these systems be used.
5. Add a screenshot of your integrity monitoring events tab.

### Feedback
Be sure to give feedback on these tasks. Do you feel these to be the kind of skills you might need or want?
