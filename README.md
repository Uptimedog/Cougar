<p align="center">
    <img alt="Cougar Logo" src="/static/logo.png?v=0.1.0" height="200" />
    <h3 align="center">Cougar</h3>
    <p align="center">Observability and Monitoring Stack.</p>
    <p align="center">
        <a href="https://github.com/Uptimedog/Cougar/releases">
            <img src="https://img.shields.io/badge/Version-v0.1.0-red.svg">
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

$ apt install docker.io
$ apt install docker-compose
$ systemctl enable docker
```

2. Run the docker containers.

```zsh
$ docker-compose up -d
```


### Grafana Agent

[Grafana Agent](https://github.com/grafana/agent) is a vendor-neutral, batteries-included telemetry collector with configuration inspired by Terraform. It is designed to be flexible, performant, and compatible with multiple ecosystems such as Prometheus and OpenTelemetry.

[Grafana Agent](https://github.com/grafana/agent) is based around components. Components are wired together to form programmable observability pipelines for telemetry collection, processing, and delivery.


1. To install the agent.

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
