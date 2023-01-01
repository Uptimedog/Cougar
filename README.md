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

1. To install the agent.

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

prometheus.remote_write "local" {
  endpoint {
    url = "http://127.0.0.1:9090/api/v1/write"
  }
}

prometheus.scrape "linux_node" {
  targets = prometheus.exporter.unix.node.targets
  forward_to = [
    prometheus.remote_write.local.receiver,
  ]
}

prometheus.scrape "demo" {
  targets = [
    // Collect metrics from the default HTTP listen address.
    {"__address__" = "127.0.0.1:12345"},
  ]
  forward_to = [prometheus.remote_write.local.receiver]
}

prometheus.exporter.unix "node" {

}
```

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
