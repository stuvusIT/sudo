# sudo

This role installs and configures sudo.
Note that root is always allowed to do anything.

## Requirements

Debian

## Role Variables

| Name               | Default/Required | Description            |
|--------------------|:----------------:|------------------------|
| `sudo_defaults`    | `{}`             | `Defaults` to set      |
| `sudo_user_rules`  | `{}`             | Per-user rules to set  |
| `sudo_group_rules` | `{}`             | Per-group rules to set |

### rules

| Name       | Default/Required   | Description                      |
|------------|:------------------:|----------------------------------|
| `host`     | `ALL`              | Host to apply this rule to       |
| `runAs`    | `ALL:ALL`          | Run-as specification for sudoers |
| `commands` | :heavy_check_mark: | Commands to allow                |

### commands

| Name      | Default/Required   | Description                             |
|-----------|:------------------:|-----------------------------------------|
| `command` | :heavy_check_mark: | Command to allow                        |
| `options` | `[]`               | List of options to set for this command |

## Example Playbook

```yml
- hosts: all
  roles:
  - sudo
     sudo_defaults:
       - env_reset
       - loglinelen=0
       - 'secure_path="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"'

     sudo_group_rules:
       wheel:
         commands:
           - command: ALL
             options:
               - NOPASSWD
               - SETENV

      sudo_user_rules:
       nagios:
         commands:
           - command: /usr/lib/nagios/plugins/check_apt
             options:
               - NOPASSWD
           - command: /usr/lib/nagios/plugins/check_pgsql
             options:
               - NOPASSWD
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Janne Heß](https://github.com/dasJ)
