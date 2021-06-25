# Custom Image mit Packer

## Voraussetzungen
In der Buildumgebung bspw. lokale Workstation muss Packer installiert und ausführbar sein. Für das Abspielen des Ansible Playbooks (provisioners_shell-ansible.json) muss neben Packer auch Ansible auf dem System vorhanden sein. Außerdem muss die Buildumgebung über einen Internetanschluss verfügen welcher ausgehend SSH-Verbindungen zulassen.

## Anpassungen
In der Datei vars.json müssen folgende Variable angepasst werden:

- username = pluscloud open Benutzer
- password = pluscloud open Benutzerkennwort
- tenant_id = pluscloud open Projekt ID

alle anderen Variablen sind bereits vorkonfiguriert um in der pluscloud open ein Custom-Image zu erzeugen.

## Erzeugen eines Custom Images
Es gibt zwei Beispieldateien 

- provisioners_shell-ansible.json 
- provisioners_shell.json 

Beide Beispiele erzeugen ein Custom-Image mit einem Webserver, bei provisioners_shell-ansible.json werden zusätzlich noch SSH-Keys über anisble im Image hinterlegt. In der Datei ./ansible/roles/install_ssh-keys/tasks/upload_pubkeys.yml können ab Zeile 9 eigene SSH Keys hinterlegt werden. Die Public SSH-Keys müssen in ./ansible/roles/install_ssh-keys/files/ abgelegt werden. Die Keys werden im Image für den Benutzer centos hinterlegt.

Durch Aufruf von:

```
packer build -var-file=vars.json provisioners_shell-ansible.json 
```
oder

```
packer build -var-file=vars.json provisioners_shell.json 
```
 wird jeweils ein Image erzeugt und im openstack Projekt der HCI abgelegt.

## Links

- [packer Builder openstack](https://www.packer.io/docs/builders/openstack)
- [packer Provisioner file](https://www.packer.io/docs/provisioners/file)
- [packer Provisioner shell](https://www.packer.io/docs/provisioners/shell)
- [ansible (Herstellerseite)](https://www.ansible.com/)
- [ansible playbook Einführung](https://docs.ansible.com/ansible/latest/user_guide/playbooks_intro.html)