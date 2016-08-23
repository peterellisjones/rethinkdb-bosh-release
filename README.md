# RethinkDB [BOSH](http://bosh.io/) Release

Supports clustering. So far only tested with Bosh Lite.

Note the compilation step takes up to 30 mins for the rethinkdb package.

Example [manifest v2](https://bosh.io/docs/manifest-v2.html) instance groups block:
```yaml
instance_groups:
  - name: rethinkdb
    instances: 3
    resource_pool: default
    persistent_disk: 1_024
    networks:
      - name: default
        static_ips:
        - 10.244.0.2
        - 10.244.0.3
        - 10.244.0.4
    jobs:
      - release: rethinkdb
        name: rethinkdb
        properties:
          rethinkdb:
            initial_password: admin
            http_port: 8080
            driver_port: 28015
            cluster_port: 29015
            cluster_ips:
            - 10.244.0.2
            - 10.244.0.3
            - 10.244.0.4
```

Default port for admin UI is 8080:

![](http://i.imgur.com/i16okKj.png)
