
# Adding an SSH Key to Your GitHub Account

This guide walks you through the steps of generating an SSH key and adding it to your GitHub account. SSH keys provide a secure way of connecting to GitHub without needing to enter your username and password every time.

## Prerequisites

- Have access to a terminal/command line
- Have a GitHub account
- Ensure `ssh-keygen` is installed on your machine

## Step 1: Create an SSH Key

1. Open your terminal.

2. Run the following command, replacing `{youremailaccount@yourdomain.com}` with your email address. This email should be the same as the one associated with your GitHub account for easy identification of the key.

    ```bash
    ssh-keygen -t rsa -b 4096 -C "{youremailaccount@yourdomain.com}"
    ```

3. When prompted to "Enter file in which to save the key," enter a custom file path to store your SSH key. Replace `{keyfilename}` with your desired filename. If you're unsure, you can just press **Enter** to use the default file location.

    ```bash
    Enter file in which to save the key (/home/user/.ssh/id_rsa): /home/user/.ssh/{keyfilename}
    ```

4. You'll be asked to enter a passphrase for an added layer of security. You can either enter a passphrase or press **Enter** to skip this step.

5. Change the permissions of your SSH key file to ensure that it is kept secure. Replace `{keyfilename}` with the name of your SSH key file.

    ```bash
    chmod 600 /home/user/.ssh/{keyfilename}
    ```

6. Add your SSH key to the SSH agent. This step ensures that your SSH key is used whenever you connect to GitHub.

    ```bash
    ssh-add -K /home/user/.ssh/{keyfilename}
    ```

## Step 2: Add Your SSH Key to Your GitHub Account

1. Copy the SSH key to your clipboard. Ensure you replace `{keyfilename}` with your actual SSH key filename.

    ```bash
    cat /home/user/.ssh/{keyfilename}.pub | pbcopy
    ```

    > **Note:** If `pbcopy` command does not work (for instance, if you are on Linux), you can use `xclip` instead. If `xclip` is not installed, you can usually install it with your package manager. For copying the key, use:

    ```bash
    cat /home/user/.ssh/{keyfilename}.pub | xclip -selection clipboard
    ```

    If you're on a system without `pbcopy` or `xclip`, simply open the `.pub` file with a text editor and manually copy the contents.

2. Open your web browser and go to your GitHub account settings, or directly navigate to [https://github.com/settings/keys](https://github.com/settings/keys).

3. Click on the **New SSH key** button.

4. In the "Title" field, enter a descriptive name for the new key. This could be the name of the computer or device you're using.

5. In the "Key" field, paste the SSH key you copied earlier.

6. Click **Add SSH key** to save the new key.

## Verifying Your Setup

After adding your SSH key to GitHub, you can verify that the setup works correctly by attempting to SSH to GitHub.

1. Open your terminal.
2. Enter the following command:

    ```bash
    ssh -T git@github.com
    ```

3. You may see a warning like this:

    ```plaintext
    The authenticity of host 'github.com (IP ADDRESS)' can't be established.
    RSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
    Are you sure you want to continue connecting (yes/no/[fingerprint])?
    ```

    Type `yes` and press **Enter**.

4. If everything is set up correctly, you should see a message like the following:

    ```plaintext
    Hi <your_username>! You've successfully authenticated, but GitHub does not provide shell access.
    ```

    This message means your SSH setup is correctly configured and you can now use SSH to connect to GitHub without having to supply your username and password.

## Troubleshooting

If you encounter any issues during this process, here are a few common troubleshooting steps:

- Ensure that you have correctly copied the entire SSH key (it should start with `ssh-rsa` or another key type and end with your email address).
- Make sure you've added the SSH key to the correct GitHub account.
- Verify that your SSH key is added to your SSH agent by running 
```bash
ssh-add -l
```

- If you don't see your key listed, add it to your SSH agent with:

```bash
ssh-add ~/.ssh/{keyfilename}
```

Make sure to replace `{keyfilename}` with the actual path to your SSH key file.

- If you are still unable to connect, check your firewall settings and ensure that outgoing connections to port 22 (the standard port for SSH) are allowed.
- GitHub's documentation also provides a comprehensive guide and troubleshooting tips for SSH issues.

Remember, maintaining the security of your SSH keys is crucial. Keep your private key secure and never share it.

## Conclusion

You have now learned how to create an SSH key, add it to your SSH agent, and add your public SSH key to your GitHub account. This will allow you to securely connect to GitHub without needing to use your username and password each time. Happy coding!

For more detailed information, you can always refer to the official GitHub documentation on SSH keys.
