1. Update the Instance names in the instance groups:
    vim configs/current_instance_groups.yaml
2. Update the group name to avoid matchings to a host name:
    vim configs/*/inventories/*/*group*
3. Update the Label's organizations and move them to the correct organization:
    vim configs/*/labels/*
    mkdir configs/Dummy/labels; for file in configs/Default/labels/*; do mv ${file} ${file/Default/Dummy}; done
4. Update the Schedules to have an organization:
    vim $(grep -lR ToDo)
5. Remove default schedules to be created:
    rm configs/schedules/[1-5]*
6. Run the playbook:
    ansible-playbook -i localhost, config-controller-filetree.yml -e "{dir_orgs_vars: $PWD/configs, orgs: Dummy, controller_configuration_credentials_secure_logging: false}" -e @/tmp/vault.yaml -e @paths.yaml
