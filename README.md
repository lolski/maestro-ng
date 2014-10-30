A simple fork of Maestro-NG that adds support for Docker's `--volumes-from` feature.

Usage:

    name: test1
    ships:
      node1:
        ip: 123.456.789.910
        docker_port: 2375
        ssh_tunnel:
          user: my_username
          key: ~/.ssh/my_private_key
          port: 22

    services:
      baseimage:
        image: phusion/baseimage
        requires: [ mysql-data ]
        instances:
          baseimage:
            ship: node1
            volumes-from:
              - baseimage-data
      baseimage-data:
        image: phusion/baseimage
        instances:
          baseimage:
            ship: node1
            volumes: 
              /where/to/be/mounted/in/container: /host/path