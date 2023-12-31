<div>
  <p align="center">
    <img width=60% src="images/gsoc.svg"> <img width=35% src="images/cncf.svg">
  </p>
</div>

# Google Summer of Code(GSoC) 2023 Final Report

**Student**：[zhy76](https://github.com/zhy76)

**Organization**: CNCF && KubeArmor

**Project**: [GitHub Actions for KubeArmor](https://summerofcode.withgoogle.com/programs/2023/projects/0EWL96Fd)

**Issue**: <https://github.com/kubearmor/KubeArmor/issues/1128>

**Code**: <https://github.com/kubearmor/kubearmor-action/tree/main>

## Introduction

<div>
  <p align="center">
    <img width=100% src="images/kubearmor-logo.webp">
  </p>
</div>

This is my first time participating in GSoC, and I am honored to be selected by CNCF and KubeArmor organization and complete this project within three months.

First of all, I am very grateful to my mentors: [Barun Acharya](https://github.com/daemon1024), [Ankur Kothiwal](https://github.com/Ankurk99), [Rahul Jadhav](https://github.com/nyrahul), [Anurag](https://github.com/kranurag7), who gave me a lot of help in the project. Their professionalism and patience are worth learning from and it was a wonderful experience to work with them.

During the project, I build a Github Action that visualizes the application's system-level behaviors and network connection changes. For example, which processes are generated by the application and the parent-child relationship between processes, which file access is generated, which network connections are generated, network connection topology, network connection changes, and so on. I think this will greatly help developers identify project problems in advance, ensure the quality of the code, avoid serious consequences, and improve the visibility of the project.

## Work Done

### Discuss the scheme and write a formal proposal

I actively participated in the discussion of the project and determined the final implementation method and effect. The core algorithm of this project is developed based on go language, for which multiple ways to publish GitHub Actions written in Go are compared: Composite actions, Pre-compiled binaries with a shim, Docker containers. I eventually chose to use Composite actions to develop Github Actions written in Go.

### Complete the entire project

Firstly, the mentor created a new code repository called [kubearmor-action](https://github.com/kubearmor/kubearmor-action), I then submitted some PRs for code architecture initialization, implementation of the entire kubearmor-action workflow and optimize the entire workflow.

I have divided the entire workflow into the following parts:

1. Setup Go
2. Checkout to your repo
3. Install a kubernetes cluster
4. Install kubearmor components
5. Deploy your application
6. Check all pods are ready, if not, get reason
7. Runs Integration/Tests/Load Generation
8. Save the application summary report and Generate visualisation results
9. Get the latest summary report file
10. Get the visualisation results
11. Store the latest summary report file
12. Store the visualisation results
13. Comment the visualisation results on the PR
14. Delete the new application

Related PRs:

- <https://github.com/kubearmor/kubearmor-action/pull/8>
- <https://github.com/kubearmor/kubearmor-action/pull/11>
- <https://github.com/kubearmor/kubearmor-action/pull/13>
- <https://github.com/kubearmor/kubearmor-action/pull/14>
- <https://github.com/kubearmor/kubearmor-action/pull/18>
- <https://github.com/kubearmor/kubearmor-action/pull/19>
- <https://github.com/kubearmor/kubearmor-client/pull/346>

### Project results display

The most difficult part of the project is the visualization of system and network behavior, which I need to represent in data structures and implement relevant differentiation algorithms.

System visualization algorithm flow:

<img width=100% src="images/system-workflow.png">

Network visualization algorithm flow:

<img width=100% src="images/network-workflow.png">

Take the sock-shop microservice demo as an example, Visualizations are as follows.

All system behaviors:

<img width=100% src="images/system-visual-all.png">

All network behaviors:

<img width=100% src="images/network-visual-all.png">

Filters Pod behavior that contains front-end：

System level：

<img width=100% src="images/system-visual-filter.png">

Network level(Contains changes in network behavior):

<img width=100% src="images/network-visual-filter.png">

## Future Work

Now running through the entire process, we can visualize system behavior and network behavior, which is a great help for Devops. In the future, we can consider adding more interesting features, such as container security issues and cluster security issues that we are currently concerned about. We can consider early detection and resolution of security issues through our Kubeararmor-action component during project development. This also requires support from upstream kubearmor and kubearmor-client.

Also, as the size of the project increases, we need to consider adding more tests.

We also welcome more people to put forward more opinions and expectations for this project.

## Conclusion

In this project, I developed a github action application using the Go language, which was able to visualize system and network behavior during development and comment on it in PR.

This is a rare experience for me to complete the development of a whole project on my own. In the project, I learned how to develop a Github Action application, Go language and Shell language development skills, eBPF knowledge, k8s related ingress and egress knowledge, etc. The most difficult part is the algorithmic part of system behavior visualization and network behavior visualization. I need to represent it with data structures and complete the algorithm of network behavior changes. At the same time, because the weekly meetings are full of English dialogue, my English oral expression and listening ability have been greatly improved.

If you want to use the project, you can follow the [README](https://github.com/kubearmor/kubearmor-action#readme) to learn how to use.
