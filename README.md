# BAR Infra

This is my own personal place to work on bar infra. When initially trying
to get into it (bar infrastructure), i was overwhelmed by the different
repositories. This is just a place for me to pull things together and
maybe test out ideas in the infrastructure.

## Just some random thoughts

### Three Repositories

There currently are three(?) ansible reposittories that build the infra. That
is ansible-monitoring, ansible-spads-setup and ansible-teiserver.

This currently leads to

* three different `ansible.cfg` files
* three different inventory scripts
* Three different ssh keys

yes, they are all(?) the same file contents but they are not the same files.

> **Note**
>
> Oh, there is actually a fourth one now: https://github.com/beyond-all-reason/ansible-live-services
> With a fourth ansible.cfg, ssh key and inventory ...


### The playbooks

There are really quite a few playbooks.

### The inventories

I like the inventories. Having a single inventory could make things a little
more choesive. E.g. in my local setup its `spads-test1` and `teiserver-test`.

Also, there are two in bash and one in python. Even though they mostly
do the same, its still three of them, in two languages.

Also, there are host_vars which rely on the names. Its confusing to get
a graps of what is what

### The roles

Within the three repository there are distinct roles, that could be refactored
intor their own repos.

* **ansible-monitoring** -> client, and monitoring
* **ansible-spads-setup** -> spads
* **ansible-teiserver** -> teiserver

I think specific role repositories could help seperate concerns and allow
for more flexible integrations in different setups. Maybe even better
testing of the roles?

### Python scripts

There are quite a few standalone python scripts all over the place. I think
having a more central way to manage all of these would be benefitial. I
recently have become quite fond of https://poethepoet.natn.io/ as a central
way to "do stuff". Whether poe or not, having a more cohesive "admin cli"
would be benefitial. A single repository could help


## Issues

### Spads installer

The  spads installer is hosted on http://planetspads.free.fr/.
The first time i tried to run the playbook failed because that site was
down. Why not use github.com as a store for the installer instead?


### Monitoring

I needed to comment out the monitoring stuff in both `roles/teiserver/tasks/main.yml`
and `roles/spads/tasks/main.yaml` to be able to run the playbook.

It could not find `ansible.builtin.import_tasks: monitoring.yml` and
`ansible.builtinimport_role: name: beyondallreason.monitoring.client`.

