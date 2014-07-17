## Prepare the Minions

* SSH into the master ssh://salt-master.knban.com

```bash
# Accept all minions
sudo salt-key -A

# Setup both minions with a base state:
# node.js, mongodb, nginx, supervisor, ssh keys
sudo salt '*' state.sls knban.base
```
