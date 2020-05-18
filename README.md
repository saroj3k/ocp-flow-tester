# Test OCP 3.11 flow matrix

This playbook is indended to test OCP 3.11 flow matrix according to [OCP 3.11 documentation](https://docs.openshift.com/container-platform/3.11/install/prerequisites.html).

## Configuration
### Installing requirements

This playbook requires ansible on the openshift installer node.
It also requires nc on all nodes. To install it you can use: `ansible-playbook -i {/path/to/your/inventory} check_flows.yml -t prerequisites`

### Openshift configuration

To test external flows, we need an additional machine. Depending on your needs and infrastructure, you could use the deploy machine (the one that runs openshift-ansible playbooks).
The machine have to be in inventory in a group called `flowexternal`.

The following example shows how to add deploy machine to inventory:
```
[flowexternal]
localhost
```

## Testing machines connectivity

Openshift must be shutted down to use this script.

### without ocp fw rules

In order to test machine connectivity, OCP and iptables must be shutted down.
 * stop iptables run following command: `ansible -b -i {/path/to/your/inventory} -m service -a "name=iptables state=stopped" nodes`

/!\ If you used firewalld, replace iptables with it /!\

When ipdables is disabled, you can follow the 'Launch checks' section.

### Launch checks

To launch the playbook, checkout it on the machine you used to run openshift-ansible playbook and run the following command: `ansible-playboot -i {/path/to/your/inventory} check_flows.yml`

Following variables can be passed to the playbook to fit your needs:
 * openshift_master_api_port: api port (default 8443)
 * openshift_dnsmasq_port: dns masq port 53 before 3.2 or update else 8053 (default 8053)
