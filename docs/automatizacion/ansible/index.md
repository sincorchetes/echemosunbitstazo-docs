# Ansible

## Playbooks

### Concepto

Los Playbooks permiten escribir guiones que permiten automatizar multitud de procesos y tareas sin tener que ir ejecutando cada uno de los comandos en modo ad-hoc en el resto de servidores.

### Formato

Los playbooks utilizan un lenguaje de datos serializado llamado YAML.

### Módulos

Son librerías desarrolladas para facilitar la gestión de determinadas tareas como la decompresión/compresión de archivos; cambios de permisos; gestión de paquetería…etc

### Aplicaciones

#### Concatenar cadena con un valor de una variable

```
"{{ '.'.join(('www',dominio))}}"</code>
```

#### Actualizar todos los paquetes

```
---
- name: Actualizar paquetería
  hosts: "{{ host }}"

  tasks:
  - name: Actualizando la paquetería del sistema
    dnf:
      name: "*"
      state: latest
```

### Crear un playbook que muestre la fecha/hora del sistema

```
---
- name: Obtener fecha/hora
  hosts: {{ host }}

  tasks:
  - name: Obtener fehca/hora del sistema
    shell: date
```

## Vault

### Encriptar datos

Ansible Vault es una funcionalidad que permite encriptar contraseñas en archivos.

#### Crear vault

```
ansible-vault create nombre_archivo
```

#### Editar información del vault

```
ansible-vault edit nombre_archivo
```

#### Usando el vault en un playbook

Incluimos el vault en el apartado `vars_files:`

```
- name: test encrypted vault file
  hosts: localhost
  connection: local

  vars_files:
    - foo_vault_file.yml

  tasks:
    - name: debug secret
      debug:
        var: my_variable
```

Ejecutamos el playbook:

```
ansible-playbook test_vault_file.yml --ask-vault-pass
```