# Sysdig agent compose setup

A simple setup to deploy Sysdig agent.

## Pre-Requisites

### Distributions

The below Linux distributions are supported by the Sysdig agent when run with an officially released kernel:

 - **Amazon Linux**: any version available from [AWS Marketplace](https://aws.amazon.com/marketplace)
 - **CentOS**: 6.0+
 - **CoreOS**: 591.0.0+
 - **Debian**: 6.0+
 - **Fedora**: 13+
 - **RHEL**: 6.0+
 - **Ubuntu**: 10.04+
 - **Oracle**: 6.0+ (UEK kernels R3+, all RHCK kernels)

If a customized or non-officially released kernel is being run, you will need to have the kernel headers installed for our agent to complete its installation.

### Network connection

A small Sysdig agent is installed into each host being monitored and will need to be able to connect to the Sysdig Monitor backend servers to report host metrics.

The agent must be able to reach the address `collector.sysdigcloud.com` (via multiple IPs) over port `6666/TCP` default.

If needed, see this [FAQ on changing the agent's port number](https://support.sysdig.com/hc/en-us/articles/204205969).

Please note that, if a proxy is in use, it must be configured to be "fully-transparent".

Non-transparent proxies will not allow the agent to connect. [For more information see this link](https://support.sysdig.com/hc/en-us/articles/204272585).

### Access key

The installation of the Sysdig agent requires an access key.

This key and the agent installation instructions are presented to you after activating your account and using a web based wizard upon initial login.

The same information can also be found in the `Settings > Agent Installation` menu of the web interface after logging in.

This access key should be set in the [.env](.env) file.

### Tags

Tagging your hosts is highly recommended.

Tags allow you to sort nodes of your infrastructure into custom groups in Sysdig Monitor.

Replace the `TAG` value in the [.env](.env) with a comma-separated list in the form of `TAG_NAME:TAG_VALUE`.

For example: `role:webserver,location:europe`.

### Kernel Module / Headers

The installation process will attempt to compile a kernel module needed for the agent to work.

If required kernel header files for the running kernel are not available, the agent installer will then attempt to download a pre-compiled kernel module from Sysdig if available.

Compiling the module is supported for all officially released kernels from the distributions listed [above](#distributions) and pre-compiled modules are available for the most recent kernels from a subset of the supported OS list above.

See this [FAQ on installing header files](https://support.sysdig.com/hc/en-us/articles/204187225) if they are missing in your AWS instance.

Some cloud hosting service providers supply pre-configured Linux instances with customized kernels. You may need to contact your provider's support desk for instructions on obtaining appropriate header files, or installing the distribution's default kernel.

## Installation

The Sysdig agent is available to run inside a single Docker container to report on the entire host (only one agent license is needed to report on all containers).

To install Sysdig agent, simply pull agent image from the Docker Hub registry and run it with these two commands:

```bash
docker-compose pull
docker-compose up -d
```

Please note that you must have downloaded this repository and completed the [.env](.env) beforehand.

If you have any issues, please refer to [the full installation instructions](http://support.sysdig.com/hc/en-us/sections/200959909) and [FAQ](http://support.sysdig.com/hc/en-us/sections/200707005) pages.

And do not hesitate to contact Sisdig support at [support@sysdig.com](mailto:support@sysdig.com)!
