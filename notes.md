
## add ssh key
Create SSH key:
   ssh-keygen -t rsa -b 4096 -C {youremailaccount@yourdomain.com}
   		Enter file in which to save the key (~/.ssh/id_rsa): ~/.ssh/{keyfilename}
   chmod 600 /Users/wwang2/.ssh/{keyfilename}
   ssh-add -K /Users/wwang2/.ssh/{keyfilename}

Add key to your github account:
open https://github.com/settings/keys click "New SSH key"


## check remote branch
git branch -r


