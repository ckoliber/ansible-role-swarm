# Ansible Role Swarm

This Ansible role sets up a Docker Swarm cluster on Linux hosts. It installs Docker, initializes the Swarm on the first manager, joins managers/workers, and creates an overlay network for services.

## Features

-   Installs Docker via `geerlingguy.docker`
-   Initializes the Swarm on the first host in the `manager` group
-   Joins additional managers and workers automatically
-   Creates an overlay network named `internal` with a configurable subnet
-   Optional cleanup of nodes in Down/Drain state
-   Idempotent and safe to run multiple times

## Requirements

-   Ansible 2.9+
-   Linux (Debian/Ubuntu/RHEL/Alma/Rocky/Fedora/Arch/Alpine/SUSE)
-   Galaxy role available: `geerlingguy.docker`

## Role Variables

Variables can be set in your playbook or inventory. See `defaults/main.yml` for all options.
OS-family specific variables can be defined in `vars/<Family>.yml` and are loaded automatically.

| Variable        | Description                                     | Default        |
| --------------- | ----------------------------------------------- | -------------- |
| `swarm_cidr`    | Overlay network CIDR for the `internal` network | `10.40.0.0/16` |
| `swarm_port`    | Swarm listen/advertise port                     | `2377`         |
| `swarm_force`   | Force new cluster on initialization             | `false`        |
| `swarm_clean`   | Remove nodes in Down/Drain state (leader only)  | `false`        |
| `swarm_manager` | Inventory group name that contains managers     | `manager`      |

Example inventory (first manager becomes leader):

```ini
[manager]
manager-1

[workers]
worker-1
worker-2
```

Example playbook:

```yaml
- hosts: all
  become: true
  roles:
      - ckoliber.swarm
```

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License

This project is licensed under the [MIT](LICENSE.md).  
Copyright (c) KoLiBer (koliberr136a1@gmail.com)
