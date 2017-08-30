# P3 api services on chestnut.mcs.anl.gov

The API services are configured using the unified deployment configuration
files that are in /vol/patric3/production (aka gitlab.cels.anl.gov:PATRIC3/production-distributions.git)

## To update configs and build a new release

First we update the configuration files. Note that the current setup includes
a commit hash for the p3_api module within the p3-api/distro.cfg file; the intent
is to have repeatable builds.

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
```

Then update the distribution manifest and check out code. Here we check out code into a date-stamped 
directory so we can keep history of the builds we've done.

```
# set up runtime environment
$ cd /vol/patric3/production/distribs/p3-api
$ . /vol/patric3/production/build/distro_utils/user-env.sh
# create updated module manifest
$ create-manifest -I ../../site-definition -I ../../cores --no-recurse
# check out code
$ checkout-from-manifest -I ../../site-definition -I ../../cores /disks/p3/production/p3-api/build-2017-0830-1 /disks/p3/production/p3-api/deployment
```

Build:

```
# Create a new shell with a clean environment
$ exit
$ bash
$ cd /disks/p3/production/p3-api/build-2017-0830-1/dev_container
# bootstrap and build
$ export KB_IGNORE_MISSING_DEPENDENCIES=1
$ ./bootstrap /disks/patric-common/runtime 
ERROR: The following modules were listed as dependencies but were not present in the modules directory:
   from module auth: jars
Ignoring missing dependencies.
Warning: missing jarfile /usr/share/java/jackson-core.jar
Warning: missing jarfile /usr/share/java/jackson-mapper.jar
$ . user-env.sh 
$ make
[much text elided]
```

Deploy:

```
# Deploy
$ perl auto-deploy deploy.cfg
```

And restart services:

```
# get a clean shell again
$ exit
$ bash
$ cd /disks/p3/production/p3-api/deployment/services/p3_api_service
$ ./stop_service
$ ./start_service
