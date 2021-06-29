# hobo-pki

To create SSL certs (from a self-signed Root CA, created the first time this play runs):

    ansible-playbook -i inventory/hostnames main.yml

## Inventory

Create a file in ./inventory that has a list of the URLs you're generating:

    $ cat ./inventory/hostnames

    www.somewhere.com
    www.anywhere.com
    www.nowhere.com
    www.everywhere.com

### What if I have a SAN (Subject Alternate Name)

You can create a directory in ./host_vars for the domain name, and add a `sans` variable with a list of the SANs that you need:

    $ cat ./host_vars/www.anywhere.com
    
    ---
    sans:
    - www.mydomain.com
    - www.mydomein.com
    - www.anotheronetoo.com

# Results

    PLAY RECAP ********************************************************************************************************
    www.anywhere.com           : ok=9    changed=7    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    www.everywhere.com         : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    www.nowhere.com            : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
    www.somewhere.com          : ok=9    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0 

# Setting up pyenv and virtualenv

    pyenv virtualenv 3.9.0 ansible-venv
    pyenv activate ansible-venv
    pip install ansible
    