---
layout: "consul"
page_title: "Provider: Consul"
sidebar_current: "docs-consul-index"
---

# Consul Provider

[Consul](http://www.consul.io) is a tool for service discovery, configuration
and orchestration. The Consul provider exposes resources used to interact with a
Consul cluster. Configuration of the provider is optional, as it provides
defaults for all arguments.

Use the navigation to the left to read about the available resources.

## Example Usage

```
# Configure the Consul provider
provider "consul" {
    address = "demo.consul.io:80"
    datacenter = "nyc1"
}

# Access a key in Consul
resource "consul_keys" "app" {
    key {
        name = "ami"
        path = "service/app/launch_ami"
        default = "ami-1234"
    }
}

# Use our variable from Consul
resource "aws_instance" "app" {
    ami = "${consul_keys.app.var.ami}"
}
```

## Argument Reference

The following arguments are supported:

* `address` - (Optional) The HTTP API address of the agent to use. Defaults to "127.0.0.1:8500".
* `datacenter` - (Optional) The datacenter to use. Defaults to that of the agent.

