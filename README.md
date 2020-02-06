# trustroots ansible setup

Ansible setup for trustroots server. This currently does not configure the whole server, just selected things we've added in. It's an incremental project.

## prerequisites

You will need:
- a modern ansible installation (probably >=2.8)
- an account on the trustroots server with sudo
- the vault password (ask [nick](https://github.com/nicksellen) over a secure channel)

You can put the put the password into a file named `vault-password` in the root directory, but preferable use a password manager with a CLI interface and write an executable script such as:

```sh
#!/bin/sh

pass trustroots/vault
```

(I would actually like to use the [passwordstore](https://docs.ansible.com/ansible/latest/plugins/lookup/passwordstore.html) module, but not everyone is using [pass](https://www.passwordstore.org/) yet...)

## standards

It tries to follow the ansible [best practises](https://docs.ansible.com/ansible/latest/user_guide/playbooks_best_practices.html) guide for directory layout and other conventions.

## tips

Use the `--step` option to run through one step at a time, with interactive confirmation at each step.

## playbooks

### mailtrain

This sets up an instance of [mailtrain](https://github.com/Mailtrain-org/mailtrain).

It uses the `development` branch, which is the v2 beta. We should change it to a stable branch or tag if one becomes availaible.

See [mailtrain.yml](mailtrain.yml) for the configuration options and values.

You can run it with:

```
ansible-playbook -K mailtrain.yml
```

(the `-K` flag is to make it ask you for your user password to gain super user access)