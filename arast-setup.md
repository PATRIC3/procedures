## The PATRIC Assembly Service Setup (ARAST)

The assembly service consists of a control server and one or more compute servers. Currently, `elm.mcs.anl.gov` 
is the master node which runs both the control server and one compute server. Multiple magellan nodes are 
configured to run as compute servers: `wasp-03`, `wasp-04`, and `wasp-05`. 

### Start/stop the master node

The start/stop scripts are on `elm` in the `/disks/arast` directory:
```
./restart.elm.sh
./stop.elm.sh
```
This will start/stop both the control server and compute server.

### List connected compute nodes

Each compute node is typically configured to run concurrent assembly workers with 4 threads/worker.

```
curl http://tutorial.theseed.org/assembly/admin/system/node; echo
[{"host": "140.221.x1.y1"}, {"host": "140.221.x2.y2"}, {"host": "140.221.x3.y3"}]
```

`elm` has 24 cores and therefore runs 6 compute workers, in addition to being the control server.

The three wasp nodes below each has 8 compute workers:
* `wasp-03` (`10.1.28.29` through SAL; no dedicated external IP; shows on control server as `x.y.64.21`)
* `wasp-04` (has external IP)
* `wasp-05` (has external IP)

To restart a wasp compute node:
```
ssh ubuntu@wasp-IP
./restart.p3.worker.sh
```

### List running and queued jobs
``` 
curl http://tutorial.theseed.org/assembly/admin/system/jobs; echo
```
