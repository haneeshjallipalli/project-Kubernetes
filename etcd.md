### Working with ETCDCTL and ETCDUTL
etcdctl is a command line client for etcd.
In all our Kubernetes hands-on labs, the ETCD key-value database is deployed as a static pod on the master. The version used is v3.

To make use of etcdctl for tasks such as backup, verify it is running on API version 3.x:

etcdctl version
Example:

controlplane ~ ➜  etcdctl version
etcdctl version: 3.5.16
API version: 3.5
Backing Up ETCD
Using etcdctl (Snapshot-based Backup)

### To take snapshot of etcd database
```
controlplane ~ ➜  etcdctl --endpoints=https://[127.0.0.1]:2379 \
--cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/server.crt \
--key=/etc/kubernetes/pki/etcd/server.key \
snapshot save /opt/snapshot-pre-boot.db
{"level":"info","ts":"2025-04-24T09:36:04.813156Z","caller":"snapshot/v3_snapshot.go:65","msg":"created temporary db file","path":"/opt/snapshot-pre-boot.db.part"}
{"level":"info","ts":"2025-04-24T09:36:04.820464Z","logger":"client","caller":"v3@v3.5.16/maintenance.go:212","msg":"opened snapshot stream; downloading"}
{"level":"info","ts":"2025-04-24T09:36:04.820534Z","caller":"snapshot/v3_snapshot.go:73","msg":"fetching snapshot","endpoint":"https://[127.0.0.1]:2379"}
{"level":"info","ts":"2025-04-24T09:36:04.853763Z","logger":"client","caller":"v3@v3.5.16/maintenance.go:220","msg":"completed snapshot read; closing"}
{"level":"info","ts":"2025-04-24T09:36:04.853939Z","caller":"snapshot/v3_snapshot.go:88","msg":"fetched snapshot","endpoint":"https://[127.0.0.1]:2379","size":"1.7 MB","took":"now"}
{"level":"info","ts":"2025-04-24T09:36:04.854024Z","caller":"snapshot/v3_snapshot.go:97","msg":"saved","path":"/opt/snapshot-pre-boot.db"}
Snapshot saved at /opt/snapshot-pre-boot.db
```

### Required Options
--endpoints points to the etcd server (default: localhost:2379)

--cacert path to the CA cert

--cert path to the client cert

--key path to the client key

### Using etcdutl (File-based Backup)
For offline file-level backup of the data directory:

etcdutl backup \
  --data-dir /var/lib/etcd \
  --backup-dir /backup/etcd-backup
This copies the etcd backend database and WAL files to the target location.

Checking Snapshot Status
You can inspect the metadata of a snapshot file using:

etcdctl snapshot status /backup/etcd-snapshot.db \
  --write-out=table
This shows details like size, revision, hash, total keys, etc. It is helpful to verify snapshot integrity before restore.

Restoring ETCD
Using etcdutl
To restore a snapshot to a new data directory:

etcdutl snapshot restore /backup/etcd-snapshot.db \
  --data-dir /var/lib/etcd-restored
To use a backup made with etcdutl backup, simply copy the backup contents back into /var/lib/etcd and restart etcd.

Notes
etcdctl snapshot save is used for creating .db snapshots from live etcd clusters.

etcdctl snapshot status provides metadata information about the snapshot file.

etcdutl snapshot restore is used to restore a .db snapshot file.

etcdutl backup performs a raw file-level copy of etcd’s data and WAL files without needing etcd to be running.
