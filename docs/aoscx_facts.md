# module: aoscx_facts

description: This module retrieves facts from Aruba devices running the AOS-CX
operating system.

Facts will be printed out when the playbook execution is done with increased
verbosity.

##### ARGUMENTS

```YAML
  gather_subset:
    description: >
      Retrieve a subset of all device information. This can be a single
      category or it can be a list. As warning, leaving this field blank
      returns all facts, which may be an intensive process.
    type: list
    elements: str
    choices:
      - config
      - domain_name
      - fans
      - host_name
      - management_interface
      - physical_interfaces
      - platform_name
      - power_supplies
      - product_info
      - resource_utilization
      - software_images
      - software_info
      - software_version
    required: false
    default:
      - domain_name
      - fans
      - host_name
      - management_interface
      - physical_interfaces
      - platform_name
      - power_supplies
      - product_info
      - resource_utilization
      - software_images
      - software_info
      - software_version
  gather_network_resources:
    description: >
      Retrieve vlan, interface, or vrf information. This can be a single
      category or it can be a list. Leaving this field blank returns all all
      interfaces, vlans, and vrfs.
    type: list
    elements: str
    choices:
      - interfaces
      - vlans
      - vrfs
    required: false
```

##### EXAMPLES

```YAML
- name: >
    Retrieve all information from the device and save into a variable
    "facts_output".
  aoscx_facts:
  register: facts_output

- name: Retrieve power supply and domain name info from the device
  aoscx_facts:
    gather_subset:
      - power_supplies
      - domain_name

- name: >
    Retrieve VRF info, host name, and fan info from the device and save into a
    variable.
  aoscx_facts:
    gather_subset:
      - fans
      - host_name
    gather_network_resources:
      - vrfs
  register: facts_subset_output
```
