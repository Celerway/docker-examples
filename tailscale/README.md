# Tailscale example

This example downloads and runs the latest build from the tailscale docker registry. 
It can be applied using config management, or the config management functions from the API.

## Requirements

* Router software >= v2.12.1
* Feature license for container-management enabled.

## Remarks

* The example defines the tailscale container as the only container to be run. This is done
  by erasing the existing configuration first (`reset_*` methods). Modify the example if this 
  is not what you want.
* We always recommend using specific versions for your containers, instead of `:latest`. This
  ensures that you know which software version the router has downloaded, and to notify the 
  router when it needs to update. Please switch the tag `:latest` with the latest static version
  tag when you want to extend on this example.

## Installation

Upload the configuration to configuration management, and apply to your router.

## Results

This will start the tailscale VPN in a container. The way the tailscale container works, 
is that it prints a URL to the docker logs (stdout) that you can visit to connect it to your
tailscale network. 

To see the output of docker logs, use the apps-logs route of the API. The name of the task 
is `tailscale_vpn`.

When you have connected the container, a new node should appear in your tailscale network. 

To make the router actually use the tailscale connection, you need to set the IP of the 
container as gateway address. That is usually 192.168.5.175, but you can also assign a 
static IP or static DHCP lease to the container for a reliable reference.
