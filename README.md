# Ansible Role: Flight Deck base

Installs base utilities and performs common configuration the [Flight Deck](https://github.com/ten7/flight-deck) set of containers.

## Requirements

* None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`).

### Creating groups

`flightdeck_groups`

Specifies the groups to create.

```yaml
flightdeck_groups:
  - name: "flighdeck"
  - name: "green"
    gid: 999
  - name: "purple"
    system: true
```

### Creating users

`flightdeck_users`

Specifies the users to create. The format is similar to [socketwench.users-and-groups](https://github.com/socketwench/ansible-role-users-and-groups).

Groups must first be created using `flightdeck_groups`.

```yaml
flightdeck_users:
  - name: "flighdeck"
    group: "flightdeck"
    home: "/home/flightdeck"
```

### Customizing the prompt

`flightdeck_root_prompt` and `flightdeck_user_prompt`

Allows you to change the default command line prompt for root, and for all other users.

### Installing packages

`flightdeck_base_packages`

Specifies a list of Alpine Linux packages to install. If not provided, `bash` will be installed.

### Customizing the entrypoint

`flightdeck_run_commands`

By default, this role will create an entrypoint script, `/usr/local/bin/docker-entrypoint.sh` for use by Docker. You can add further commands by specifying them in this variable:

```yaml
flightdeck_run_commands: |
    ansible-playbook -i /ansible/inventories/all.ini /ansible/run.yml
```

## Dependencies

None.

## Example Playbook

Add the role to a playbook which is run during a `docker build`.

    - hosts: docker
      roles:
         - role: ten7.flightdeck_base

## License

GPL v3

## Author Information

This role was created by [TEN7](https://ten7.com/).
