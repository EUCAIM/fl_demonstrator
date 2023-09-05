# How to deploy Substra for EUCAIM

A network is **already** deploy on the Owkin side. The objective of the EUCAIM deployment is to deploy **new backends** and **frontends** to connect to this already existing network. This deployment needs a **Kubernetes** cluster up and running per backend.

The documentation provides a [**How to guide to deploy Substra**](https://docs.substra.org/en/0.30.0/operations/walkthrough.html). As we are in a case where part of this deployment already exists, some of this guide can be skipped. The different steps of the guide are listed below with some additional instructions.

The existing network correspond to the bundle version **Substra 0.30.0.** Cf here to find all component version compatible with the **0.30.0** version → [Compatibility table](https://docs.substra.org/en/0.30.0/additional/release.html)

### Steps of the EUCAIM deployment are detailed below

**Step 1:** follow to install the pre-requisites <https://docs.substra.org/en/0.30.0/operations/walkthrough/10-prerequisites.html>

**Step 2:** skip the orchestrator deployment

**Step 3:** deploy a backend: [Link](https://docs.substra.org/en/0.30.0/operations/walkthrough/30-backend-deployment.html)

Link to [Substra-backend 0.40.0](https://github.com/Substra/substra-backend/releases/tag/0.40.0).

**Additional info for step 3:**

→ to *Configure your connection to the orchestrator. In the `backend-ingen-values.yaml` file add the following content:*

```yaml
orchestrator:
 host: orchestrator.eucaim.cg.owkin.tech
 port: 9000
 mspID: <yourMspId>
```

→ to *Configure your Substra-Channels. In the `backend-values.yaml` file, add the following content under the `orchestrator` key:*

```yaml
channels:
  - channel-1:
      restricted: false
      model_export_enabled: true
      chaincode:
        name: substracc
```

→ No TLS is setup for this POC, you can skip this part

**Step 4:** to link the different backend, this step need a coordination in order to exchange secrets between the backends that need to communicate with each other. For this step, please contact the Owkin team in order to synchronize the backend configuration.

This can be achieved either at deployment time or when the backend is already deployed.

For context, the step is described here: [Link](https://docs.substra.org/en/0.30.0/operations/walkthrough/40-connect-organizations.html)

**Step 5:** deploy the frontend: [Link](https://docs.substra.org/en/0.30.0/operations/walkthrough/50-frontend-deployment.html)

Link to [Substra-frontend 0.44.0](https://github.com/Substra/substra-frontend/releases/tag/0.44.0).

**Step 6:** Ignore mutual TLS for this POC
