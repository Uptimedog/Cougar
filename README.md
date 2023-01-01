<p align="center">
    <img alt="Cougar Logo" src="/static/logo.png?v=0.4.0" height="200" />
    <h3 align="center">Cougar</h3>
    <p align="center">Observability and Monitoring LGTM Stack</p>
    <p align="center">
        <a href="https://github.com/Uptimedog/Cougar/releases">
            <img src="https://img.shields.io/badge/Version-v0.4.0-red.svg">
        </a>
        <a href="https://github.com/Uptimedog/Cougar/blob/main/LICENSE">
            <img src="https://img.shields.io/badge/LICENSE-MIT-blue.svg">
        </a>
    </p>
</p>


### Usage

1. Install docker and docker-compose.

```zsh
$ apt-get update
$ apt-get upgrade -y

$ apt install docker.io docker-compose -y
$ systemctl enable docker
```

2. Run the docker containers.

```zsh
$ docker-compose up -d
```


### Grafana Agent

[Grafana Agent](https://github.com/grafana/agent) is a vendor-neutral, batteries-included telemetry collector with configuration inspired by Terraform. It is designed to be flexible, performant, and compatible with multiple ecosystems such as Prometheus and OpenTelemetry.

1. To install the agent in a flow mode.

```zsh
$ wget https://github.com/grafana/agent/releases/download/v0.39.1/grafana-agent-flow-0.39.1-1.amd64.deb
$ dpkg -i grafana-agent-flow-0.39.1-1.amd64.deb
```

2. Update config file

```zsh
$ vim /etc/grafana-agent-flow.river
```

```hcl
logging {
    level = "debug"
}

prometheus.remote_write "default" {
  endpoint {
    url = "http://127.0.0.1:9090/api/v1/write"

    basic_auth {
      username = "admin"
      password = "password"
    }
  }
}

prometheus.scrape "linux_node" {
  scrape_interval = "15s"
  targets = prometheus.exporter.unix.node.targets
  forward_to = [
    prometheus.remote_write.default.receiver,
  ]
  metrics_path = "/metrics"
}

prometheus.scrape "agent" {
  targets = [
    {"__address__" = "127.0.0.1:12345"},
  ]
  forward_to = [
    prometheus.remote_write.default.receiver
  ]
}

prometheus.exporter.unix "node" {
  set_collectors = [
    "vmstat",
    "filesystem",
    "cpu",
    "uname",
    "diskstats",
    "loadavg",
    "meminfo",
    "netstat",
  ]
  enable_collectors = [
    "processes",
    "systemd",
  ]
  include_exporter_metrics = true
}
```

The above [configurations are shared on this link](https://grafana.github.io/agent-configurator/?c=Ly8gV2VsY29tZSB0byB0aGUgR3JhZmFuYSBBZ2VudCBDb25maWd1cmF0b3IhCi8vIFlvdSBjYW4gcGFzdGUgeW91ciBjb25maWd1cmF0aW9uIGhlcmUgb3Igc3RhcnQgYnkgdXNpbmcgdGhlIGNvbmZpZ3VyYXRpb24gd2l6YXJkIG9yIGJ5IGxvYWRpbmcgYW4gZXhhbXBsZSBmcm9tIHRoZSBjYXRhbG9nLgoKbG9nZ2luZyB7CiAgICBsZXZlbCA9ICJkZWJ1ZyIKfQoKcHJvbWV0aGV1cy5yZW1vdGVfd3JpdGUgImRlZmF1bHQiIHsKICBlbmRwb2ludCB7CiAgICB1cmwgPSAiaHR0cDovLzEyNy4wLjAuMTo5MDkwL2FwaS92MS93cml0ZSIKCiAgICBiYXNpY19hdXRoIHsKICAgICAgdXNlcm5hbWUgPSAiYWRtaW4iCiAgICAgIHBhc3N3b3JkID0gInBhc3N3b3JkIgogICAgfQogIH0KfQoKcHJvbWV0aGV1cy5zY3JhcGUgImxpbnV4X25vZGUiIHsKICBzY3JhcGVfaW50ZXJ2YWwgPSAiMTVzIgogIHRhcmdldHMgPSBwcm9tZXRoZXVzLmV4cG9ydGVyLnVuaXgubm9kZS50YXJnZXRzCiAgZm9yd2FyZF90byA9IFsKICAgIHByb21ldGhldXMucmVtb3RlX3dyaXRlLmRlZmF1bHQucmVjZWl2ZXIsCiAgXQogIG1ldHJpY3NfcGF0aCA9ICIvbWV0cmljcyIKfQoKcHJvbWV0aGV1cy5zY3JhcGUgImFnZW50IiB7CiAgdGFyZ2V0cyA9IFsKICAgIHsiX19hZGRyZXNzX18iID0gIjEyNy4wLjAuMToxMjM0NSJ9LAogIF0KICBmb3J3YXJkX3RvID0gWwogICAgcHJvbWV0aGV1cy5yZW1vdGVfd3JpdGUuZGVmYXVsdC5yZWNlaXZlcgogIF0KfQoKcHJvbWV0aGV1cy5leHBvcnRlci51bml4ICJub2RlIiB7CiAgc2V0X2NvbGxlY3RvcnMgPSBbCiAgICAidm1zdGF0IiwKICAgICJmaWxlc3lzdGVtIiwKICAgICJjcHUiLAogICAgInVuYW1lIiwKICAgICJkaXNrc3RhdHMiLAogICAgImxvYWRhdmciLAogICAgIm1lbWluZm8iLAogICAgIm5ldHN0YXQiLAogIF0KICBlbmFibGVfY29sbGVjdG9ycyA9IFsKICAgICJwcm9jZXNzZXMiLAogICAgInN5c3RlbWQiLAogIF0KICBpbmNsdWRlX2V4cG9ydGVyX21ldHJpY3MgPSB0cnVlCn0=)

3. Start the grafana agent service

```zsh
$ systemctl start grafana-agent-flow
$ systemctl status grafana-agent-flow
```


### Deploying Badger

[Badger](https://github.com/Uptimedog/Badger) is a microservice that can be used for testing the LGTM stack. To deploy badger, do the following

```zsh
$
```


### Versioning

For transparency into our release cycle and in striving to maintain backward compatibility, Cougar is maintained under the [Semantic Versioning guidelines](https://semver.org/) and release process is predictable and business-friendly.

See the [Releases section of our GitHub project](https://github.com/Uptimedog/Cougar/releases) for changelogs for each release version of Cougar. It contains summaries of the most noteworthy changes made in each release. Also see the [Milestones section](https://github.com/Uptimedog/Cougar/milestones) for the future roadmap.


### Bug tracker

If you have any suggestions, bug reports, or annoyances please report them to our issue tracker at https://github.com/Uptimedog/Cougar/issues


### Security Issues

If you discover a security vulnerability within Cougar, please send an email to [hello@clivern.com](mailto:hello@clivern.com)


### Contributing

We are an open source, community-driven project so please feel free to join us. see the [contributing guidelines](CONTRIBUTING.md) for more details.


### License

© 2023, Clivern. Released under [MIT License](https://opensource.org/licenses/mit-license.php).

**Cougar** is authored and maintained by [@clivern](http://github.com/clivern).
