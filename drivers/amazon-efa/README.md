# Amazon EC2 EFA network driver

## Installation

See [Installing Extensions](https://github.com/siderolabs/extensions#installing-extensions).

## Usage

See [Amazon EFA driver](https://github.com/amzn/amzn-drivers/tree/master/kernel/linux/efa) documentation for more information.
The driver is already built and installed in this extension, so ignore the build instructions in the documentation.

The module is not autoloaded, so the machine configuration has to ask for it:

```yaml
machine:
  kernel:
    modules:
      - name: efa
```

The device appears as `/dev/infiniband/uverbs0` on an instance type that carries
an EFA interface. Instance types without one load the module and expose nothing.
