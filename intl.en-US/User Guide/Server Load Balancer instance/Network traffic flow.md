# Network traffic flow {#concept_ev3_wsm_vdb .concept}

As a traffic forwarding service, SLB forwards requests from clients to backend servers through SLB clusters. Then, the backend servers return responses to SLB through the intranet.

## Inbound network traffic flow {#section_fxh_xgn_vdb .section}

SLB distributes incoming traffic according to the forwarding rules configured on the console or by using APIs. The following figure shows the inbound network traffic flow.

![](../DNSLB11827830/images/2333_en-US.png "Inbound network traffic flow")

1.  For TCP/UDP protocols and HTTP/HTTPS protocols, the incoming traffic must be forwarded through the LVS cluster first.
2.  A massive number of access requests are evenly distributed among all servers in the LVS cluster. Servers synchronize sessions to guarantee high availability.
    -   For Layer-4 listeners \(the frontend protocol is UDP or TCP\), the node servers in the LVS cluster distribute requests directly to backend ECS instances according to the configured forwarding rules.
    -   For Layer-7 listeners \(the frontend protocol is HTTP\), the node servers in the LVS cluster first distribute requests to the Tengine cluster. Then, the node servers in the Tengine cluster distribute the requests to backend ECS instances according to the configured forwarding rules.
    -   For Layer-7 listeners \(the frontend protocol is HTTPS\), the request distribution is similar to the HTTP protocol. However, before distributing requests to backend ECS instances, the system will call the Key Server to validate certificates and decrypt data packets.

## Outbound network traffic {#section_jcv_ghn_vdb .section}

SLB communicates with backend ECS instances through the intranet.

-   If backend ECS instances only need to handle the traffic distributed from SLB, no public bandwidth \(EIP, NAT Gateway, and public IP\) is required, and you do not need to purchase any public bandwidth.

    **Note:** ECS instances of the previous generation are directly allocated with public IP addresses. You can view the public IP addresses by using the ifconfig command. If these ECS instances process requests only through SLB, no traffic fee is incurred for traffic sent through the Internet even traffic statistics are read at the public network interface \(NIC\).

-   If you want to provide external services through backend ECS instances, or backend ECS instances need to access the Internet, you must configure at least one of the following: a public IP address, an EIP, or a NAT Gateway.

The following figure shows the outbound network traffic flow.

![](../DNSLB11827830/images/2335_en-US.png "Outbound network traffic flow")

-   For outbound traffic from SLB instances \(that is, traffic transferred through the Internet\), traffic is sent at speeds dependent on the current network capacity, and is charged. However, you are not charged for intranet communications, such as traffic transferred between SLB instances and backend ECS instances.
-   For outbound traffic from an EIP or from NAT Gateway \(that is, traffic transferred through the Internet\), traffic is sent at speeds dependent on the current network capacity, and is charged. Additionally, if an ECS instance is configured with a public IP address when it is created, the outbound traffic from this instance is also charged.
-   SLB supports dynamic access to the Internet. Specifically, if a backend ECS instance needs to access the Internet, you must first configure a public IP address for it \(by using an EIP or using NAT Gateway\) and add it to the instance.
-   A public IP address \(configured when you create an ECS instance\), EIP, and NAT gateway all allow mutual Internet access. That is, ECS instances can access the Internet or be accessed from the Internet through any of these. Note, however, that they cannot forward traffic or balance traffic loads.

