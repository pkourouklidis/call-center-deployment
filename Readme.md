This repository contains the deployment charts and configuration for the call centre demo system.

## Project Structue

There are two deployment charts within this repository that correspond to the two major architectural elements of the call centre demo system. These are the call-centre-dashboard chart and the call-centre-digital-twin chart respectively.

Each of the deployment charts contain subcharts for the different components, although the configuration that will need to be customised can be found in the parent chart's values.yaml file and only the parent chart needs to be deployed.

## Updating component version

The deployment of this system uses tagged releases.

To make a release for a specific component, you will need to create a new tag in the respective repository of the format v[0-9].[0-9].[0-9]. This will result in a new container image being pushed to the container registry and this container image will be tagged with the same tag.

To deploy the new component version, first find the subchart for the component and update the appVersion field inside of Chart.yaml. Once this has been done, you can proceed with the instructions below.

## Upgrade or Install

To install the charts you will need a namespace in a Kubernetes cluster available. In this example, the namespace is called project-call-centre.

To install both charts, execute the following commands:

```
cd call-centre-dashboard
helm dependency build
helm -n project-call-centre upgrade --install dashboard .
cd ..

cd call-centre-digital-twin
helm dependency build
helm -n project-call-centre upgrade --install digitaltwin .
cd ..
```