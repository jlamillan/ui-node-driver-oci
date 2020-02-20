# rancher-ui-driver-oci

Rancher UI driver for the [OCI docker-machine driver](https://github.com/oci/docker-machine-driver-oci)

## Usage

Manual installation is not required in [Rancher](https://rancher.com/products/rancher/) [v2.2.0+](https://forums.rancher.com/t/rancher-release-v2-2-0/) as the OCI Node Driver is included.

See the following guide for notes on installing Rancher and configuring the OCI Node Driver.

* <https://www.oci.com/docs/applications/containers/how-to-deploy-kubernetes-on-oci-with-rancher-2-2/>

Advanced usage is also discussed, including integration with OCI Kubernetes Addons:

* [OCI Container Storage Interface](https://github.com/oci/oci-blockstorage-csi-driver/) (for provisioning [Block Storage](https://www.oci.com/blockstorage))
* [OCI Cloud Controller Manager](https://github.com/oci/oci-cloud-controller-manager) (for provisioning [NodeBalancers](https://www.oci.com/nodebalancers))

### Docker Machine Driver OCI

The [OCI Docker Machine Driver](https://docs.docker.com/machine/drivers/oci/) that this Node Driver uses is described here:

* <https://www.oci.com/community/questions/17797/using-the-oci-docker-machine-driver>

## Setup

These steps are still useful in Rancher v2.0.x where the OCI Node Driver is not already included.

* Add a Machine Driver in Rancher 2.0.x (Global -> Node Drivers)
  * Name: `OCI`
  * Download URL:

    `https://github.com/oci/docker-machine-driver-oci/releases/download/v0.1.7/docker-machine-driver-oci_linux-amd64.zip`

  * Custom UI URL (Note: v0.3.0-alpha.1 and greater require Rancher 2.2.3+ ):

    `https://oci.github.io/rancher-ui-driver-oci/releases/v0.2.0/component.js`

  * Checksum

    `faaf1d7d53b55a369baeeb0855b069921a36131868fe3641eb595ac1ff4cf16f`

  * Whitelist Domains:

    `oci.github.io`

* Wait for the driver to become "Active"
* Go to Clusters -> Add Cluster, the driver and custom UI should show up.

## Development

This package contains a small web-server that will serve up the custom driver UI at `http://localhost:3000/component.js`.  You can run this while developing and point the Rancher settings there.

* `npm start`
* The driver name can be optionally overridden: `npm start -- --name=oci`
* The compiled files are viewable at <http://localhost:3000>.
* **Note:** The development server does not currently automatically restart when files are changed.
* Do not use the `model.ociConfig` signature to access your driver config in the template file, use the `config` alias that is already setup in the component

## Building

For other users to see your driver, you need to build it and host the output on a server accessible from their browsers.

* `npm run build`
* Copy the contents of the `dist` directory onto a webserver.
  * If your Rancher is configured to use HA or SSL, the server must also be available via HTTPS.

### Contribution Guidelines

Would you like to improve the `rancher-ui-driver-oci` module? Please start [here](https://github.com/oci/rancher-ui-driver-oci/blob/master/.github/CONTRIBUTING.md).

## Resources

### Announcements and Documentation

* [Now Available: OCI Rancher Integration](https://blog.oci.com/2019/04/10/now-available-oci-rancher-integration/)
* [How to Deploy Kubernetes on OCI with Rancher 2.2](https://www.oci.com/docs/applications/containers/how-to-deploy-kubernetes-on-oci-with-rancher-2-2/)
  * [OCI Container Storage Interface](https://github.com/oci/oci-blockstorage-csi-driver)
  * [OCI Cloud Controller Manager](https://github.com/oci/oci-cloud-controller-manager)

### Join us on Slack

For general help or discussion, join the [Kubernetes Slack](http://slack.k8s.io/) channel [#oci](https://kubernetes.slack.com/messages/CD4B15LUR).
