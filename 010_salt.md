We are going to build and launch a SaaS app today. The name is knban and it will live at knban.com

Knban will be an app for software teams to organize issues from many repos on one kanban board.

## Prepare the Servers

* Spin 2 VPS's @ http://digitalocean.com
  - One to run Strider-CD -- name it strider
  - One to run Knban app -- name it knbanapp01
* Configure DNS @ http://cloudflare.com
* Make each host a salt minion

```bash
SALT_MASTER_FQDN="salt-master.knban.com"

echo $(nslookup $SALT_MASTER_FQDN | grep -A1 'Name:' | grep Address | awk -F': ' '{print $2}')$'\t'"salt" | tee -a /etc/hosts

echo deb http://ppa.launchpad.net/saltstack/salt/ubuntu `lsb_release -sc` main | sudo tee /etc/apt/sources.list.d/saltstack.list

wget -q -O- "http://keyserver.ubuntu.com:11371/pks/lookup?op=get&search=0x4759FA960E27C0A6" | sudo apt-key add -

sudo apt-get update

sudo apt-get install -y salt-minion
```
