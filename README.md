<div align="center">
  <a href="https://opc-router.com/?utm_source=GitHub&utm_medium=HelmChart&utm_campaign=OpcRouterChartSample">
    <img src="img/opc_router_logo.png" alt="Logo" >
  </a>
    <br />
    <br />
  <h1 align="center">OPC Router Helm Chart Sample Project</h1>
  <p align="center">
    A sample project for kubernetes deployment of the opc router with the helm chart.
    <br />
    <a href="https://opc-router.com/?utm_source=GitHub&utm_medium=HelmChart&utm_campaign=OpcRouterChartSample"><strong>OPC Router</strong></a>
    -
    <a href="https://www.opc-router.com/contact-and-support/?utm_source=GitHub&utm_medium=HelmChart&utm_campaign=OpcRouterChartSample"><strong>Contact</strong></a>
    <br />
    <br />
  </p>
</div>

# About the Sample
## **Contents**
- [About the Sample](#about-the-sample)
  - [**Contents**](#contents)
  - [**General Information**](#general-information)
    - [**What is the sample doing?**](#what-is-the-sample-doing)
- [Getting Started](#getting-started)
  - [**Prequisites**](#prequisites)
  - [**Installation**](#installation)
  - [**Uninstalling**](#uninstalling)

## **General Information**
> This is a project sample for the opc router helm chart.
> It is for demonstrating how to deploy a opc router project from a git repository with the helm chart.
> [Read more about the OPC Router Helm Chart here.](https://github.com/OPC-Router/helm-charts)

### **What is the sample doing?**
- This sample is a fully functional OPC Router 4 project sample.
- It is a very simple project that will periodically write a file in the home directory of the docker container it is deployed in.
- The written file is a text file containing the string of an environment variable and a random number.
- The environment variable is declared in the config.yaml and initialized in the helm install command parameters.

# Getting Started

## **Prequisites**
- Kubernetes 1.12+
- Helm 3.1.0

## **Installation**
[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:
```shell
helm repo add opc-router https://opc-router.github.io/helm-charts
```
If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
<alias>` to see the charts.

You can now install this project on any kubernetes cluster using the helm chart with this command:
```shell
$ helm install my-opcrouter opc-router/opc-router \
  --set project.projectRepo=https://github.com/OPC-Router/helm-sample-project.git \
  --set project.Path=Sampleproject.rpe \
  --set project.configPath=config.yaml \
  --set envVars[0].Config="This is a random number: " \
  --set I_do_accept_the_EULA=true
```
This command will install the opc router with standard settings, as a service with a seperate mongodb container. The mongodb won't require authentification, which is not recommended. Accepting the [End User License Agreement](https://www.opc-router.com/terms-of-use-and-eula/) by setting `I_do_accept_the_EULA` to true is required for the OPCRouter to run.

## **Uninstalling**
The chart with the name `my-opcrouter` can simply be uninstalled by executing:
```shell
$ helm uninstall my-opcrouter
```
However, keep in mind that the persitant volumes of the mongodb container don't get deleted by this. When reinstalling the chart under the same name you will have to use the previous mongodb root password and replica set key or delete the persistant volume beforehand.