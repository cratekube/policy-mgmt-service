# Overview
The `policy-mgmt-service` will provide compliance information for all infrastructure provisioned through platform services. The service will be configured with a set of rules that will be applied against resource requests. It is expected that this service will be called by the `cloud-mgmt-service` and the `cluster-mgmt-service` and provide enough information for these services to deploy and manage compliant resources.

The MVP will target AWS and provide default policies for the management service MVPs. Authentication will be set at runtime using a shared token, to be superseded by more robust authentication in the future.

# Components
The following architecture is compromised of multiple components.

## policy-mgmt-service
The primary service in this architecture. See [Overview](#overview) for roles and responsibilities.

## cloud-mgmt-service
A [microservice](https://github.com/cratekube/cloud-mgmt-service) developed by the CrateKube team responsible for provisioning and monitoring cloud resources and services. The service will request policy requirements from the `policy-mgmt-service` prior to provisioning new resources.

## cluster-mgmt-service
A [microservice](https://github.com/cratekube/cluster-mgmt-service) developed by the CrateKube team responsible for providing everything needed for creating, monitoring and deleting a Kubernetes cluster and configuring it post-bootstrap. The service will request policy requirements from the `policy-mgmt-service` prior to creating and configuring a cluster.

# Diagrams

## Component
![Component](https://www.plantuml.com/plantuml/img/ZT3D2i8m30Vm-vuYxDuNs44cNXq8dcJi4DiuY-q-sbGGsRlRRWTXg7WC_oI_aD8pEWxMP0FA6xO4-Q4tMZwWmYwMbZg68xcxbfJ3CmEeXpaNjhKi_98q8CG6wjEssZTGW2DKFhOgP3oZZpjJienFsGHlQsVweBvJCiLhoUdsoedxU4W1Oo2doQ-Su9dSBsbkM5k6BdzI9NKgll45)
<details><summary>Show UML Code</summary>
<p>

```
@startuml
package "Policy Management Service" {
  [policy-mgmt-service] --> [YAML] : reads
  database "YAML" {
  }
}
package "Cloud Management Service" {
  [cloud-mgmt-service] -right-> [policy-mgmt-service] : queries
}
package "Cluster Management Service" {
  [cluster-mgmt-service] -left-> [policy-mgmt-service] : queries
}
@enduml
```

</p>
</details>

## Physical
![Component](https://www.plantuml.com/plantuml/img/fP4x2y8m58Nt_8fBzonEuY25u2H2mL4SGdejmJng7e98_hjfYY_iKF1iWO_pvN1h7xWBKIj2XBAnXMh35XNS2UGOso9KswM7Hl5miau3Kz47T4zYIC_5cNSPRAoIuWOxRl9JemcmHtUL0Z_f8OU-a5HtEb0_CiSNaU2tcfM_pMWk8xwBWTBrj19MS8de9FgtVCfT9i-p5_GV_pW-aKHgD6q-p0C0)
<details><summary>Show UML Code</summary>
<p>

```
@startuml
cloud "EC2" {
    node "K8s Platform Cluster" {
        package "Policy Management Service" {
            [policy-mgmt-service]
        }
        package "Cloud Management Service" {
            [cloud-mgmt-service] --> [policy-mgmt-service] : queries
        }
        package "Cluster Management Service" {
            [cluster-mgmt-service] --> [policy-mgmt-service] : queries
        }
    }
}
@enduml
```

</p>
</details>

## Security
![Component](https://www.plantuml.com/plantuml/img/fP5D2y8m38Rl-nLXPtiN3pBOKOI1npcaT7KRwyTeKqL7_xlTfk14c61kIHxUl4aIYzIWao9IkkGGxzOMCa7nh8s4L3YBtCJGHn2YewobLO0oBHfsWprL8PLS8HoukJIClyWXycwaYAma4ZlrZwf7tN9reWxhkoz6sC_5Kw5TkQ0DEHkecNO1n3HLZMJxqsZOm5k1hMh4pleW_TtJU8YbZTc4VTegzLNzvUffoKS9LsNurGC0)
<details><summary>Show UML Code</summary>
<p>

```
@startuml
node "K8s Platform Cluster" {
    package "Policy Management Service" {
        [policy-mgmt-service\n{token_authz}]
    }
    package "Cloud Management Service" {
         [cloud-mgmt-service] -right-> [policy-mgmt-service\n{token_authz}] : {token_authc,https}   
    }
    package "Cluster Management Service" {
        [cluster-mgmt-service] -down-> [policy-mgmt-service\n{token_authz}] : {token_authc,https}
    }
}
@enduml
```

</p>
</details>
