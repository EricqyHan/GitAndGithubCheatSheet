\*Setting up GitHub and Git on PC

- Section 11: Github: The Basics

Setting up Github on PC:
Open Terminal and enter `ls -al ~/.ssh`

Paste text below, substutiting email address
`ssh-keygen -t ed25519 -C "email addresss"`

Enter below to add your SSH key to the sssh-agent:

- `eval "$(ssh-agent -s)"`

Now check if

- `open ~/.ssh/config`

-If file does not exist then
`touch ~/.ssh/config`

open your ~/.ssh/config file and modify the file to contain following lines.
`Host * AddKeysToAgent yes UseKeychain yes IdentityFile ~/.ssh/id_ed25519 `

Add your SSH private key to the ssh-agent and store your passpharase in the keychain.

Now add SSH key to your account in github
`pbcopy < ~/.ssh/id_ed25519.pub`
