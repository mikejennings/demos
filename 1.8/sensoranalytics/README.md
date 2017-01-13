# Fast Data: Sensor Analytics

This demo is all about gaining insights from sensor streaming data.



- Estimated time for completion:
 - Single command: 10min
 - Manual: 25min
 - Development: unbounded
- Target audience: Anyone interested stream data processing and analytics with Apache Spark.

**Table of Contents**:

- [Architecture](#architecture)
- [Prerequisites](#prerequisites)
- Install the demo:
 - [Single command](#single-command)
 - [Manual](#manual)
- [Use](#use) the demo
 - [Generating transactions](#generating-transactions)
 - [Consuming transactions](#consuming-transactions)
- [Development and testing](#development)

## Architecture

## Prerequisites

- A running [DC/OS 1.8.7](https://dcos.io/releases/1.8.7/) or higher cluster with at least 4 private agents and 1 public agent each with 2 CPUs and 5 GB of RAM available as well as the [DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed in version 0.14 or higher.
- The [dcos/demo](https://github.com/dcos/demos/) Git repo must be available locally, use: `git clone https://github.com/dcos/demos.git` if you haven't done so, yet.
- The JSON query util [jq](https://github.com/stedolan/jq/wiki/Installation) must be installed.
- [SSH](https://dcos.io/docs/1.8/administration/access-node/sshcluster/) cluster access must be set up.

Going forward we'll call the directory you cloned the `dcos/demo` Git repo into `$DEMO_HOME`.

The DC/OS services and support libraries used in the demo are as follows:

- TBD

We're using the Open Data Aarhus [real-time traffic  data](https://www.odaa.dk/dataset/realtids-trafikdata) kindly provided by the Aarhus Kommune (Denmark, Europe), available via the CC Open Data license. Open Data rocks!

An [exemplary snapshot](example_data.json) is available here in this repo. This snapshot was created using the following command:

```bash
$ curl -o example_data.json https://www.odaa.dk/api/action/datastore_search?resource_id=b3eeb0ff-c8a8-4824-99d6-e0a3747c8b0d&limit=5
```

Note that the data source is updated roughly every 5 min, something to be taken into account when showing the demo.

## Install

TBD

### Single command

TBD

### Manual

#### Kafka

Install the Apache Kafka package with the following [options](kafka-config.json):

```bash
$ cd $DEMO_HOME/1.8/sensoranalytics/
$ dcos package install kafka --options=kafka-config.json
```

Note that if you are unfamiliar with Kafka and its terminology, you can check out the respective [101 example](https://github.com/dcos/examples/tree/master/1.8/kafka) as well now.

Next, figure out where the broker is:

```bash
$ dcos kafka connection

{
  "address": [
    "10.0.3.178:9398"
  ],
  "zookeeper": "master.mesos:2181/dcos-service-kafka",
  "dns": [
    "broker-0.kafka.mesos:9398"
  ],
  "vip": "broker.kafka.l4lb.thisdcos.directory:9092"
}
```

Note the FQDN for the broker, in our case `broker-0.kafka.mesos:9398`.

### Spark

Install the Apache Spark package:

```bash
$ dcos package install spark
Installing Marathon app for package [spark] version [1.0.6-2.0.2]
Installing CLI subcommand for package [spark] version [1.0.6-2.0.2]
New command available: dcos spark
DC/OS Spark is being installed!

        Documentation: https://docs.mesosphere.com/current/usage/service-guides/spark/
        Issues: https://docs.mesosphere.com/support/
```

### Zeppelin

Install the Apache Zeppelin package:

```bash
$ dcos package install zeppelin
Installing Marathon app for package [zeppelin] version [0.5.6]
DC/OS Zeppelin is being installed!

        Documentation: https://docs.mesosphere.com/zeppelin/
        Issues: https://docs.mesosphere.com/support/
```

## Use

The following sections describe how to use the demo after having installed it.

TBD

## Development

If you are interested in testing this demo locally or want to extend it, follow the instructions in this section.


### Tunneling

For local development and testing we use [DC/OS tunneling](https://dcos.io/docs/1.8/administration/access-node/tunnel/) to make the nodes directly accessible on the development machine. The following instructions are only an example (using Tunnelblick on macOS) and the concrete steps necessary depend on your platform as well as on what VPN client you're using.

```bash
$ sudo dcos tunnel vpn --client=/Applications/Tunnelblick.app/Contents/Resources/openvpn/openvpn-2.3.12/openvpn
```

Note that it is necessary to [add the announced DNS servers]( https://support.apple.com/kb/PH18499?locale=en_US) as told by Tunnelblick, and make sure the are they appear at the top of the list, before any other DNS server entries.

### WIP

- fetcher from HTTP-API into Kafka
- using [integration](https://spark.apache.org/docs/latest/streaming-kafka-0-10-integration.html) to read out from spark
- using Zeppelin as the front-end


## Discussion

Should you have any questions or suggestions concerning the demo, please raise an [issue](https://dcosjira.atlassian.net/) in Jira or let us know via the [users@dcos.io](mailto:users@dcos.io) mailing list.