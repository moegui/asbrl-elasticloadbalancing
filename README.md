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
  - SECURITY_GROUPS: (List)
    - NAME: (String)
- LISTENERS: (List)
  - NAME: (String)
  - LB_NAME: (String)
  - TARGET_NAME: (String)
- TARGETS:
  - NAME: (String)
  - LB_NAME: (String)
  - HEALTH_CHECK:
    - PORT:
      - ENABLED: False (Default)
    - PATH:
      - ENABLED: False (Default)


Dependencies
------------

None

Example Playbook
----------------

          - name: Generate {{EnvironmentType}} cf-loadbalancer
            include_role:
              name: asbrl-elasticloadbalancing
            vars:
              TEMPLATE_DEST: ./artifacts/{{EnvironmentType}}/cf-rabbitstack-loadbalancer.yml
              TAGS:
                RELEASE: "{{Release}}"
                ENVIRONMENT_TYPE: "{{EnvironmentType}}"
              LOAD_BALANCERS:
              - NAME: Rabbit
                SECURITY_GROUPS:
                - NAME: ALBInternal
                - NAME: ALBCustom
              LISTENERS:
              - NAME: Client
                LB_NAME: Rabbit
                TARGET_NAME: Client
              - NAME: Mng
                LB_NAME: Rabbit
                TARGET_NAME: Mng
              TARGETS:
              - NAME: Client
                LB_NAME: Rabbit
                HEALTH_CHECK:
                  PORT:
                    ENABLED: true
                  PATH:
                    ENABLED: true
              - NAME: Mng
                LB_NAME: Rabbit

            
License
-------

BSD

Author Information
------------------

Moegui.com
