# Network management

Subnet management is available via menu `Inventory -> Subnets`. You can proceed with basic CRUD operations for subnets. All subnets have to be defined in CIDR format (e.g. 192.168.5.0/24). Every subnet should have default credentials attached. Credentials can be defined preliminary or created while you are editing/creating subnet (by pressing <i class="fa fa-plus-square"></i> near corresponding dropdown).

# Exclusions

!!! note
    You can exclude only end-point IP-addresses. At this moment there's no way to exclude subnet from a bigger network. You can exclude particular nodes or to split bigger network to smaller segments.

!!! success "Note"
    When IP-address is excluded, corresponding node is removed from all tasks.