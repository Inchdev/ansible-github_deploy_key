Role Name
=========

This role allows you to add or remove a ssh key from your github repository deploy key using the github api : https://developer.github.com/v3/repos/keys/

Requirements
------------

None

Role Variables
--------------

The variables that can be passed to this role and a brief description about them are as follows:
````
github_deploy_key_readonly: true # Whether the deploy key should be read only

github_api_url: https://api.github.com/repos/{{github_repository}}/keys # This should not be overwritten, it is used to resolve the github api url

deploy_key_operation: present # present: Add a key, absent: remove a key

github_deploy_key_name: ansible-generated # The title of your key

github_deploy_key: ssh-rsa foobar # The content of your key (required)


# You can either authenticate with your username and password (if 2FA is disabled) :
github_username: myUsername
github_password: myPassword

# Or use the preferred way, authentication token that you can create here : https://github.com/settings/tokens

github_access_token: myAccessTokenThatIsSuperLongAndUsuallyInTheVault

````

Dependencies
------------

None

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: github_deploy_key
          vars:
            github_repository: owner/repo_name
            github_access_token: 932042631839424hrkrhiyfg871y89
            github_deploy_key: ssh-rsa tototata
            github_deploy_key_readonly: false

    - hosts: servers
      roles:
        - role: github_deploy_key
          vars:
            github_repository: owner/repo_name
            github_username: myUsername
            github_password: myPassword
            github_deploy_key: ssh-rsa tototata
    
    - hosts: servers
      roles:
        - role: github_deploy_key
          vars:
            deploy_key_operation: absent
            github_repository: owner/repo_name
            github_deploy_key_id: 4242
            github_access_token: 932042631839424hrkrhiyfg871y89

License
-------

BSD

Author Information
------------------

https://github.com/Uelb
