<p align="center">
    <img alt="Cougar Logo" src="/static/logo.png?v=0.8.0" height="200" />
    <h3 align="center">Cougar</h3>
    <p align="center">Observability and Monitoring LGTM Stack</p>
    <p align="center">
        <a href="https://github.com/Uptimedog/Cougar/releases">
            <img src="https://img.shields.io/badge/Version-v0.8.0-red.svg">
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

### Grafana Alloy

To install and run `alloy` on hosts

```zsh
$ wget https://github.com/grafana/alloy/releases/download/v1.0.0/alloy-linux-amd64.zip
$ unzip alloy-linux-amd64.zip
$ mv alloy-linux-amd64 alloy

$ export REMOTE_LOKI_WRITE_URL=http://X.X.X.X:3100/loki/api/v1/push
$ export REMOTE_PROMETHEUS_WRITE_URL=http://X.X.X.X:9090/api/v1/write
$ export REMOTE_PROMETHEUS_USERNAME=admin
$ export REMOTE_PROMETHEUS_PASSWORD=password

$ ./alloy run config.alloy
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
