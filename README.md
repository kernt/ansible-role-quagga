# Ansible Role: Quagga

A brief description of the role goes here.

## Requirements

None

## Role Variables

Available variables are listed below, with their default values (see `defaults/main.yml`)

    quagga_vtysh_password: zebra
    quagga_zebra_log: /var/log/quagga/zebra.log
    quagga_ospfd_log: /var/log/quagga/ospfd.log
    quagga_ospfd_log_precision: 0
    quagga_ospfd_enabled: "False"
    quagga_ospfd_reference_bw: 100

Only the zebdra daemon is eanbled by default within the role.  To enable ospfd set `quagga_osfpd_enabled` to `True`.  The default logging locations can be overriden.  The default precision for both zebra and ospfd is set to the quagga default.  The OSPF reference bandwidth is configured to the default of 100mbit.

    quagga_ospfd:
        router_id: 192.168.29.1
        networks:
            - prefix: 192.168.29.0/24
              area: 0
        interfaces:
            - name: eth0
              passive: "True"

The `quagga_ospfd` hash will contain the information needed configure OSPF on a host.  The `router_id` is the OSPF router-id for the host.  The `networks` key contains a list of `prefix` and `area` that will be advertised via OSPF.  The interfaces matching the given prefix will have OSPF enabled on them.  OSPF will send out hello packets and form neighbor relationships over these interfaces.  The `interfaces` key contains optional config items in a list.  The `name` is required to set either `passive` or `cost`.  The `passive` key is not required and is to allow the setting of an interface as passive.

## Dependencies

None

## Example Playbook

    - hosts: ospf-routers
      roles:
         - { role: dselders.quagga }

## License

BSD

## Author Information

Created by [David Selders](https://github.com/dselders)
