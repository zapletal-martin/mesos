---
layout: documentation
---

# Deploy Scripts

Mesos includes a set of scripts in `MESOS_HOME/deploy` that can be used to deploy it on a cluster. To use these scripts, you need to create two configuration files: `MESOS_HOME/conf/masters`, which should list the hostname(s) of the node(s) you want to be your masters (one per line), and `MESOS_HOME/conf/slaves`, which should contain a list of hostnames for your slaves. You can then start a cluster with `deploy/start-mesos` and stop it with `deploy/stop-mesos`.

It is also possible to set environment variables, ulimits, etc that will affect the master and slave. by editing `MESOS_HOME/deploy/mesos-env.sh`. One particularly useful setting is `LIBPROCESS_IP`, which tells the master and slave binaries which IP address to bind to; in some installations, the default interface that the hostname resolves to is not the machine's external IP address, so you can set the right IP through this variable.

Finally, the deploy scripts do not use ZooKeeper by default. If you want to use ZooKeeper (for multiple masters), you can do so by either editing `deploy/mesos-env.sh` to set `MESOS_URL` to a `zoo://` or `zoofile://` URL, or by editing `conf/mesos.conf` to set the `url` configuration parameter. Please see the "High Availability" documentation for details.

## Notes

* The deploy scripts assume that Mesos is located in the same directory on all nodes.
* If you want to enable multiple Unix users to submit to the same cluster, you need to run the Mesos slaves as root (or possibly set the right attributes on the `mesos-slave` binary). Otherwise, they will fail to `setuid`.