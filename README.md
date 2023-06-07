# autotag-ghaction-job
Before using read this document entirely.

To use it in your repository simply copy the file file [.github/workflows/autotag.yml](.github/workflows/autotag.yml) 
and the directory `release/` especially script file [release/tag-next-version.sh](release/tag-next-version.sh).

!Warning [autotag.yml](.github/workflows/autotag.yml) workflow assumes that script `tag-next-version.sh` is located in a `release` directory.
If you want to change the location you must edit a workflow also.

## ATTENTION - Prerequisite

Because of some github action optimisation [discussed here](https://github.com/orgs/community/discussions/27028)
tags simply created and pushed by github action doesn't trigger builds that are subscribed on push tags.

To overcome this issue the workflow use deployment key feature of GITHUB.

Therefore to use this workflow follow the steps below

1. Create keys
```bash
ssh-keygen -t ed25519 -f deploy-key -N "" -q -C ""
```
3. Add the pub key as `deploy key`
   - Copy the entire content of the file `deploy-key.pub`
   - go to repository on github
   - enter the settings
   - from left menu choose `Deploy keys`
   - click the button `Add deploy key`
   - enter the name for the key (what ever you like, just to be meaningful for you) ex. autotag
   - paste the content you have copied from `deploy-key.pub` to `Key` section
   - !important! check the checkbox `Allow write access`
   - Click `Add key`
4. Store private key as github secrets `DEPLOYMENT_KEY`
   - Copy the entire content of the file `deploy-key`
   - go to repository on github
   - enter the settings
   - from left menu choose `Secrets and variables` and from submenu `Actions`
   - ensure you are on a `Secrets` tab
   - Click `New repository secret`
   - Enter the name `DEPLOYMENT_KEY`
   - paste the content you have copied from `deploy-key` to `Secret` section
   - Click `Add secret`

And after that the workflow should work as expected.
