# Zigbee2MQTT config for microshift (OpenShift/Kubernetes)

I store my [zigbee2mqtt](https://www.zigbee2mqtt.io)
service setup here. I run it on
[microshift](https://github.com/openshift/microshift) which is minimalistic
[kubernetes](https://kubernetes.io/) distro based on
[OpenShift](https://openshift.com). My HW is RaspberryPi 4.

This is very simple sample. I put it here as I found it tough to configure
access to usb serial zigbee stick. I went by using a helper to get access
to device,
[generic device plugin](https://github.com/squat/generic-device-plugin)
made the access easy. Just a line in StatefulSet: `squat.ai/serial: 1`.

I just dump the config files here, let's see if it makes a point to
do any further helm or anything. Probably not. Hopefully this helps
someone else to run a service on restricted kube that requires device access.

# Install:

1. install the generic device plugin:
   `oc apply -f https://raw.githubusercontent.com/squat/generic-device-plugin/main/manifests/generic-device-plugin.yaml`
2. Modify the cm.yaml to have your mqtt server and token.
3. Make route address to suite yours in route.yaml
1. `oc apply -f ...` for each yaml here.
   * **ns.yaml**: Namespace
   * **cm.yaml**: Configuration file for z2m 
   * **pvc.yaml**: Persistent storage to store your data
   * **svc.yaml**: Service for the pod
   * **route.yaml**: Publish route for the service
   * **ss.yaml**: Create the pod using StatefulSet so it is monitored

Good luck, and happy home hacking!
