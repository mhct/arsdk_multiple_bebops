##ARSDK to connect to multiple Bebops

This repository contains the binary libraries needed to connect one server with multiple network adapters to multiple Bebop drones.

The patch applied to compile the binaries, simply consists in binding the connections to a particular IP, which is configured via a environment variable "LOCAL_DRONE_IP"

The patched files changed the SDK behaviour of binding to all adapters to bind to only one IP. Thus, any libraries used in the SDK which have code like:
`recvSin.sin_addr.s_addr = htonl(INADDR_ANY);`

were rewriten to  something like:
`const char* local_drone_ip = getenv("LOCAL_DRONE_IP");
recvSin.sin_addr.s_addr = inet_addr (local_drone_ip);`

If you want to test, you can download the **lib** folder from this repository.
At the source of your bebop_autonomy workspace, copy the downloaded **lib** folder to **devel/.private/bebop_driver/arsdk/out/arsdk-native/staging/usr/lib**.

## Execution
Before loading the bebop driver you have to export the environment variable
`export LOCAL_DRONE_IP=192.168.42.xx` 

where 192.168.42.xx is the IP of you adapter connected to the bebop.



