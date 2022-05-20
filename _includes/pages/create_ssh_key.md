### Create SSH Keys

SSH (Secure Shell) keys are acces credentials that are used in the SSH protocol and are foundational to modern Infrastructure-as-a-Service platforms such as AWS, Google Cloud, and Azure. Procedure is as follows:

1. Start a Bash Shell

1. Create a Service Account SSH Key as follows:

    ```
    ssh-keygen -t rsa -b 4096 -C "olympus@demo.com" -f $HOME/.ssh/olympus
    ```
    
    Command prompts and output are as follows:
    
    ```
    Generating public/private rsa key pair
    Enter file in which to save the key (~/.ssh/olympus):
    Enter passphrase (empty for no passphrase):
    Your identification has been saved in ~/.ssh/olympus
    Your public key has been saved in ~/.ssh/olympus.pub
    ```

1. Create a Personal SSH Key as follows:

    ```
    ssh-keygen -t rsa -b 4096 -C "YOUR EMAIL ADDRESS"
    ```
    
    Command prompts and output are as follows:

    ```
    Generating public/private rsa key pair
    Enter file in which to save the key (~/.ssh/id_rsa):
    Enter passphrase (empty for no passphrase):
    Your identification has been saved in ~/.ssh/id_rsa
    Your public key has been saved in ~/.ssh/id_rsa.pub
    ```

1. Set SSH Permissions

    ```
    chmod -R 700 ~/.ssh
    chmod 644 ~/.ssh/authorized_keys
    ``` 

1. Safeguard both SSH Keys