# Network management

Subnet management is available via menu `Inventory -> Subnets`. You can proceed with basic CRUD operations for subnets. All subnets have to be defined in CIDR format (e.g. 192.168.5.0/24). Every subnet should have default credentials attached. Credentials can be defined preliminary or created while you are editing/creating subnet (by pressing <i class="fa fa-plus-square"></i> near corresponding dropdown).

In subnet form there's flag `discoverable`. Marking it as `yes` will allow Java daemon to scan this subnet trying to discover new or existing nodes. Setting this flag to `no` will exclude this subnet from [discovery task](discovery.md) and will display <i class="fa fa-warning text-danger"></i> next to network address in subnet list.

# Exclusions

!!! note
    You can exclude only end-point IP-addresses. At this moment there's no way to exclude subnet from a bigger network. You can exclude particular nodes or to split bigger network to smaller segments.

!!! success "Note"
    Node with IP from exclusions' list will not be discovered nor processed by any tasks in Java daemon