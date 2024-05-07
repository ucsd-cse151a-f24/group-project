# Group Project Information

## Login to SDSC Expanse
Go to `portal.expanse.sdsc.edu` and login with your "access-ci.org" or "ucsd.edu" credentials.

> **For first-time login:**
>
> Click on the "expanse shell access" icon box. Once you are in terminal you will need to add the following linked folders: 
```bash
# Create a new folder with your username 
# and add symbolic link
ln -sf /expanse/lustre/projects/uci150/$USER

# Add symbolic link to `esolares` folder where 
# the singularity images are stored
ln -sf /expanse/lustre/projects/uci150/esolares

# To see your group members folders, do the following
# for each group member's usernames
ln -sf /expanse/lustre/projects/uci150/GROUPMEMBERUSERNAME
```

## Support
If you are having trouble, please submit a ticket to https://support.access-ci.org/.
