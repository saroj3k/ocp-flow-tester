# Test OCP 3.11 flow matrix

This playbook is indended to test OCP 3.11 flow matrix according to [OCP 3.11 documentation](https://docs.openshift.com/container-platform/3.11/install/prerequisites.html).

## Installing requirements

This playbook requires ansible on the openshift installer node.
It also requires nc on all nodes. To install it : `ansible-playboot -i {/path/to/your/inventory} check_flows.yml -t prerequisites`

## Testing machine sconnectivity

### without ocp fw rules

In order to tes tmachine connectivity, OCP and iptables must be shutted down.
 * stop iptables run following command: `ansible -b -i {/path/to/your/inventory} -m service -a "name=iptables state=stopped" nodes`

/!\ If you used firewalld, replace iptables with it /!\

When ipdables is disabled, you can follow the 'Launch checks' section.

### Launch checks

To launch the playbook, checkout it on the machine you used to run openshift-ansible playbook and run the following command: `ansible-playboot -i {/path/to/your/inventory} check_flows.yml`
