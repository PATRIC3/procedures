# P3 api services on chestnut.mcs.anl.gov

The API services are configured using the unified deployment configuration
files that are in /vol/patric3/production (aka gitlab.cels.anl.gov:PATRIC3/production-distributions.git)

## To update configs and build a new release

```
$ cd /vol/patric3/production/site-definition

# Create a shell to isolate PATH and variable setup
$ bash
$ ls
auth-definitions.tt   db-definitions.tt   db-passwords.tt   global-config.tt   host-definitions.tt   macros.tt
auth-definitions.tt~  db-definitions.tt~  db-passwords.tt~  global-config.tt~  host-definitions.tt~  macros.tt~
# Edit desired config file
$ cd /vol/patric3/production/distribs/p3-api
# edit distro.cfg to change configuration of the service
# set up runtime environment
$ . /vol/patric3/production/build/distro_utils/user-env.sh
# create updated module manifest
$ create-manifest -I ../../site-definition -I ../../cores --no-recurse
# check out code
$ checkout-from-manifest -I ../../site-definition -I ../../cores /disks/p3/production/p3-api/build-2017-0830-1 /disks/p3/production/p3-api/deployment/

# Create a new shell with a clean environment
$ exit
$ bash

```
