Database Server Role
====================

Deze Ansible rol installeert de MySQL-server op Ubuntu 24.04, stelt een externe verbinding in en maakt een gebruiker aan met opgegeven rechten.

Requirements
------------

- Ubuntu 24.04 met `apt`
- Poort 3306 moet bereikbaar zijn voor clients (bijv. vanaf je webservers)
- MySQL roottoegang via `unix_socket` (standaard bij Ubuntu)

Role Variables
--------------

| Variabele         | Default waarde | Beschrijving                                        |
|-------------------|----------------|-----------------------------------------------------|
| `mysql_user`      | `dbuser`       | De gebruikersnaam die wordt aangemaakt              |
| `mysql_password`  | `dbpassword`   | Het wachtwoord van deze gebruiker                   |

Deze variabelen zijn gedefinieerd in `defaults/main.yml`, maar je kunt ze eenvoudig overschrijven in je playbook of via `group_vars`.

Dependencies
------------

- Deze rol vereist dat de pakketten `mysql-server` en `python3-pymysql` geïnstalleerd worden (gebeurt automatisch).
- De MySQL-service wordt automatisch gestart en geconfigureerd om verbindingen van buitenaf toe te staan (`bind-address = 0.0.0.0`).

Example Playbook
----------------

`example.yaml`
- name: Installeer database via Galaxy
  hosts: dbservers
  become: yes
  roles:
    - jhuijgen83.dbserver

Example Inventory
-----------------

De gebruiker moet een eigen `inventory.ini` aanmaken. Voorbeeld:

`example.ini`
[dbservers]
192.168.1.20 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
