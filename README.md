ASBRL-ELASTICLOADBALANCING
=========

Create a CloudFormation Template to Deploy a Load Balancer Stack

Requirements
------------

None


Role Variables
--------------

- TEMPLATE_DEST: (String)
- TAGS:
    - RELEASE: (String)
    - ENVIRONMENT_TYPE: (String)
- LOAD_BALANCERS: (List)
  - NAME: (String)
  - TYPE: application | gateway | network
  - SCHEME: internal | internet-facing
  - ATTRIBUTES:
    - KEY: (String)
    - VALUE: (String)
- LISTENERS: (List)
  - NAME: (String)
  - PORT: (Number)
  - PROTOCOL: GENEVE | HTTP | HTTPS | TCP | TCP_UDP | TLS | UDP
  - LB_NAME: (String)
  - TARGET_NAME: (String)
- TARGETS:
  - NAME: (String)
  - LB_NAME: (String)
  - PORT: (Number)
  - PROTOCOL: GENEVE | HTTP | HTTPS | TCP | TCP_UDP | TLS | UDP
  - HEALTH_CHECK:
    - INTERVAL: (Number)
    - PORT: (Number)
    - PROTOCOL: GENEVE | HTTP | HTTPS | TCP | TCP_UDP | TLS | UDP
    - TIMEOUT: (Number)
  - HEALTHY_THRESHOLD_COUNT: (Number)
  - UNHEALTHY_THRESHOLD_COUNT: (Number)
  - ATTRIBUTES:
    - KEY: (String)
    - VALUE: (String)


Dependencies
------------

None

Example Playbook
----------------

          - name: Generate {{EnvironmentType}} cf-loadbalancer
            include_role:
              name: asbrl-elasticloadbalancing
            vars:
              TEMPLATE_DEST: ./artifacts/{{EnvironmentType}}/cf-mongostack-loadbalancer.yml
              TAGS:
                RELEASE: "{{Release}}"
                ENVIRONMENT_TYPE: "{{EnvironmentType}}"
              LOAD_BALANCERS:
              - NAME: Mongo
                TYPE: network
                SCHEME: internet-facing
              LISTENERS:
              - NAME: Client
                PORT: 27017
                PROTOCOL: TCP
                LB_NAME: Mongo
                TARGET_NAME: Client
              TARGETS:
              - NAME: Client
                LB_NAME: Mongo
                PORT: 27017
                PROTOCOL: TCP
                HEALTH_CHECK:
                  INTERVAL: 30
                  PORT: 27017
                  PROTOCOL: TCP
                  TIMEOUT: 10
                HEALTHY_THRESHOLD_COUNT: 3
                UNHEALTHY_THRESHOLD_COUNT: 3
            
License
-------

GPL-3.0-only


Author Information
------------------

Moegui.com
