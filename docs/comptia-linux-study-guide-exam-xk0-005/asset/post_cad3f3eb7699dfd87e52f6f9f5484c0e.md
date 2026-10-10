
## Chapter 30: Orchestrating the Environment

1. A, B, C, D, E. All these choices contain items that can use orchestration and are correct choices. Since orchestration refers to the organization of a process that is balanced and coordinated and achieves consistency in the results, there are not many things that cannot use orchestration. An exception would be a situation where you are trying to simulate random chaos.

2. B. To meet Connie’s requirement, the development environment must be immutable (not modifiable). Therefore, option B is the correct answer. Self-replication will not assist in reaching Connie’s requirement for an unchanging environment, so option A is a wrong answer. Kubernetes is an orchestration engine, not an attribute, so option C is also an incorrect choice. Infrastructure as code does not provide an unchanging environment, so option D is a wrong answer. In orchestration, self-healing refers to a different issue than an unchanging environment, so option E is also an incorrect choice.

3. D. With container orchestration and DevOps, to keep the production and development environment matching so that problems do not occur when an app is moved into production, you simply replace the old production environment with the development environment. In the case of containers, this means you stop the old production container and start the new development container as the production container in its place. Thus, option D is the correct answer and follows the “replace, not update” attribute. While the answer in option A would work, it is terribly tedious, time-consuming, and full of potential problems. Therefore, it is a wrong answer. The answer in option B is the old-school method of moving an app into production, and it does not meet Connie’s desire for a static and matching environment. Thus, it is also an incorrect answer. If before the app is ready for production, you stop any software updates on the development container from occurring, that does not make the development environment match the production environment alone. Thus, option C is a wrong choice. Option E also would work but is even more tedious and full of potential problems than the answer in option A. Therefore, it too is an incorrect choice.

4. C. Replication allows an orchestrated container to be built and deployed in multiple copies automatically. This provides high availability when a container crashes as well as when a new app container is being deployed. Therefore, option C is the correct answer. Immutability prevents environment issues from causing application problems, but it is not the best property of high availability, and thus, option A is a wrong answer. Version control allows you to roll back and troubleshoot problems in a production environment, which does help provide higher availability, but again it’s not the best attribute toward doing so. Therefore, option B is also an incorrect answer. Option D provides speed in the orchestrated environment, which also helps provide high availability to an app user, but it too is not the best advocate. Thus, option D is also a wrong answer. While documentation helps in the troubleshooting process and slightly contributes to higher availability, it is not the best either. Therefore, option E is also an incorrect choice.

5. E. *Infrastructure as code* is an umbrella term that encompasses both the configuration management settings (operating system, libraries, additional software) and the policy as code items (security policies, authentication settings). Thus, option E is the correct choice. Marathon is the orchestration tool used with the Mesos application. Therefore, option A is a wrong answer. Build automation uses infrastructure as code. Thus, option B is an incorrect answer. A development environment can be built using *infrastructure as code*. Therefore, option C is also a wrong answer. A container also can be built using *infrastructure as code* but is not the code itself, so option D is an incorrect choice too.

6. B. Ms. Ward is using build automation. Thus, option B is the correct answer. Monitoring comes after containers are deployed, so option A is a wrong choice. Replication is part of the process Ms. Ward used, but it does not describe the container deployment, so option C is not the best answer and is an incorrect choice. Version control was hopefully used by Ms. Ward so she can roll back or troubleshoot her application, if needed, but option D is not a correct answer. Docker Swarm is an orchestration system, and thus, option E is also an incorrect answer.

7. A, B, C, E. In container orchestration, automated configuration management allows containers to be deployed and replicated automatically (build automation). Also, troubleshooting *infrastructure* issues is easier because the modifications are tracked in a version control system. Thus, options A, B, C, and E are all correct answers. While automated configuration management and orchestrated containers may be part of continuous software delivery, they are not directly related. Therefore, option D is the only incorrect choice.

8. A. Mr. Abbott needs an orchestration tool that can perform self-healing. Therefore, option A is the correct answer. Build automation may be involved in self-healing, but it does not describe the ability to deploy and replicate containers after they have crashed. Thus, option B is a wrong answer. Continuous integration is a DevOps software revision control method that encourages quickly integrating app changes into the main branch. Therefore, option C is an incorrect answer. *Infrastructure as code* may be employed by build automation but does not describe the ability to self-heal. Thus, option D is a wrong choice. Pods are a component of the Kubernetes orchestration engine. Thus, option E is also an incorrect choice.

9. B, C, D, E. App container performance, metrics, container health, and default states are all collected, watched, or used by an orchestration monitoring tool. Therefore, options B, C, D, and E are all correct answers. Option A is the only incorrect choice because the version control system is not used or watched by an orchestration monitoring utility.

10. B, C. Those who chose agentless orchestration monitoring tools typically do not want to install monitoring software (an agent) on their app containers. Also, they are concerned about this installed agent adversely affecting performance. Therefore, options B and C are the correct answers. Since the answers in options A and D are opposite of options B and C, they are wrong answers. Also, the industry is divided on which is the best to use (agent or agent-less) for orchestration monitoring, so option E is also an incorrect choice.

## Index

- **A**
  - aa- complain command, 457, 635
  - disable command, 457, 635
  - enforce command, 457, 635
  - status command, 456
  - unconstrained command, 456–457
  - absolute path, 341
  - access and authentication
    - about, 499
    - answers to review questions, 869–871
    - exam essentials, 499–500
    - managing access permissions, 442–445
    - pluggable authentication modules (PAMs), 470–482
    - public key infrastructure (PKI), 483–485
    - remote access, 629–630
    - review questions, 501–502
    - Secure Shell (SSH), 486–498
    - troubleshooting access, 624–631
    - using virtual private networks (VPNs) as a client, 498–499
  - Access Control Lists (ACLs)
    - about, 448–450
    - advanced permissions and, 633–635
    - providing access control, 518–520
    - unrestricting, 682–683
  - access server (SSH), 33–34
  - accessibility, setting up, 245–247
  - AccessX, 247
  - account interface, 472
  - AccuracySec directive, 190
  - active/passive, 213
  - add chaddr command, 532
  - add command, 531–532
  - address parameter, 206
  - Address Resolution Protocol (ARP), 585
  - addrlable1 parameter, 206
  - Advanced Host Controller Interface (ACHI) driver, 673
  - advanced permissions, 633–635
  - After directive, 164
  - agent monitoring tools, 821
  - agentless monitoring tools, 821
  - aggregation, 212
  - alias command, 166, 409
  - Allman, Eric, 504
  - Also directive, 166
  - American Standard Code for Information Interchange (ASCII), 270
  - anconda file, 797–798
  - annotated tags, 762
  - Ansible, 820
  - answers
    - assessment test, IV–Xxii
    - to review questions
      - access and authentication methods, 869–871
      - application and hardware issues, 883–885
      - Bash scripts, 885–887
      - boot process, 841–844
      - cloud and virtualization concepts, 890–893
      - file/protection, 863–864
      - file/directory management, 833–837
      - firewall, 872–874
      - graphical user interface (GUI), 851–854
      - job automation, 866–888
      - kernel modules, 866–867
      - Linux devices, 881–883
      - localization, 855–858
      - logging, 871–872
      - network connections, 848–851
      - orchestration, 894–895
      - ownership and permissions, 868–869
      - performance optimization, 878–879
      - security, 874–876
      - services, 830–832
      - software, 864–866
      - storage, 861–863
      - system properties and remediation, 876–878
      - system startup and services, 844–848
      - text, 837–840
      - user issues, 880–881
      - users and groups, 858–861
      - version control, 889–890
  - Apache Handler project, 35
  - Apache web server, 22
