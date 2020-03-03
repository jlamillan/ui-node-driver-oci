# rancher-ui-driver-oci

Rancher UI driver for the [Oracle Cloud Infrastructure (OCI) rancher-machine driver](https://github.com/rancher-plugins/rancher-machine-driver-oci)

## Usage

Manual installation is not required in [Rancher](https://rancher.com/products/rancher/) [v2.4.0+](https://forums.rancher.com/t/rancher-release-v2-4-0/) as the OCI Node Driver will be included.

## Setup

If the OCI Node Driver is not inluded as a built-in driver:

* Add a Machine Driver in Rancher (Global > Node Drivers)
  * Download URL:

    `https://github.com/rancher-plugins/rancher-machine-driver-oci/releases/download/v1.0.0/rancher-machine-driver-oci-darwin`

  * Custom UI URL:

    `https://cdn.jsdelivr.net/gh/rancher-plugins/ui-node-driver-oci@v1.0.0/dist/component.js`


  * Whitelist Domains:

    `jsdelivr.net`

* Wait for the driver to download and become "Active"
* Click the user profile button in the upper right corner and add OCI Cloud Credentials
* Create a Node Template using your cloud credentials and information from OCI
* Create an "Oracle Cloud Infrastructure" cluster with node pools using the node template

## Development

This package contains a small web-server that will serve up the custom driver UI at `http://localhost:3000/component.js`.  You can run this while developing and point the Rancher settings there.

* `npm start`
* The driver name can be optionally overridden: `npm install && npm start -- --name=oci`
* The compiled files are viewable at <http://localhost:3000>.
* **Note:** The development server does not currently automatically restart when files are changed.
* Do not use the `model.ociConfig` signature to access your driver config in the template file, use the `config` alias that is already setup in the component

## Building

For other users to see your driver, you need to build it and host the output on a server accessible from their browsers.

* `npm run build`
* Copy the contents of the `dist` directory onto a webserver.
  * If your Rancher is configured to use HA or SSL, the server must also be available via HTTPS.

### Contribution Guidelines

### Announcements and Documentation
