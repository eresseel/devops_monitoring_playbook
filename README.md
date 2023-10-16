# devops_monitoring_playbook

## 1. Prepare developer environment
```bash
python3 -m venv .venv
. .venv/bin/activate
pip3 install -r requirements.txt
ansible-galaxy collection install -r ./collections/requirements.yml -p ./collections
ansible-galaxy role install -r ./roles/requirements.yml -p ./roles
ansible-vault decrypt ./files/vagrant/id_rsa
```

## 2. Vagrant VM create
```bash
vagrant up grafana
```

## 3. Development provision
```bash
ansible-playbook -i ./inventories/development/hosts grafana.yml
```

## 4. Production provision
```bash
ansible-vault decrypt ./inventories/production/group_vars/all/vault.yml
ansible-playbook -i ./inventories/production/hosts grafana.yml
```

## 5. Vagrant VM destroy
```bash
vagrant destroy -f grafana
```
