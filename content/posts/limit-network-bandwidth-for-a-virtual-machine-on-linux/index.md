+++
title = 'Limit Network Bandwidth for a Virtual Machine on Linux'
date = 2022-11-02 11:52:38.696000
+++


{{< figure src="./images/Screenshot_from_2022_11_02_11_51_58_49f1f7aeb7.png" alt="linux terminal snippet" class="center" >}}

Something very useful - find the name of the virtual NIC on the host, and run a magical tc command:

```bash
# ip l | grep vnet
47: vnet1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc htb master virbr0 state UNKNOWN mode DEFAULT group default qlen 1000
# tc class change dev vnet1 classid 1:1 root htb rate 100Mbit
```

Here is an example of me using it to choke Steam:

![steam_tc.png](./images/steam_tc_3633038547.png)