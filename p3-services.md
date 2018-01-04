# Monitoring and restarting PATRIC Services

## Web Services

### Restarting Web server (p3_web)
Production webserver is hosted in harad (BI machine)
```bash
// connect to harad.vbi.vt.edu
$ sudo -u patric bash -l
$ cd ~/prod/p3_web
$ forever restart bin/p3-web
```

### Restarting User service (p3_user)
```bash
// connect to harad.vbi.vt.edu
$ sudo -u patric bash -l
$ cd ~/prod/p3_user
$ forever restart bin/p3-user
```

### Restarting API service (p3_api)
```bash
// connect to chestnut.mcs.anl.gov
$ sudo -u p3 bash -l
$ cd /disks/p3/production/p3-api/deployment/services/p3_api_service/
$ ./stop_service
$ ./start_service
```

### Restarting Index worker
```bash
// move to p3_api deployment
$ ./stop_worker
$ ./start_worker
```

### Restarting Solr
```bash
// connect to chestnut.mcs.anl.gov
$ sudo -u p3 bash -l
$ cd /disks/p3/deployment/services/p3_solr_service/
$ ./stop_service
$ ./start_service
```

## Workspace
```bash
// connect to beech
$ sudo -u p3 bash -l
$ cd /disks/p3/deployment/services/Workspace/
$ ./stop_service
$ ./start_service
```

## Service workers

### Services using AWE
```bash
// monitoring workers
// connect to redwood.mcs.anl.gov
$ ps auxw | grep awe-cli

// restarting workers
// connect to beech.mcs.anl.gov
$ sudo -u p3 bash -l
$ cd /disks/p3/deployment/services/app_service/
$ ./stop_service
$ ./start_service
```

### Similar Genome Finder
```bash
// connect to larch.mcs.anl.gov
$ sudo -u p3 bash -l
$ cd /disks/p3/deployment/services/similarity_service/
$ ./stop_service
$ ./start_service
```

### BLAST
```bash
//
```

### See more detail
```
https://github.com/PATRIC3/procedures/blob/master/system_startup/beech.mcs.anl.gov
```