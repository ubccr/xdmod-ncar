# xdmod-ncar

The NCAR module delivers a customized SUPReMM realm dataset mapping file that
supports the Ganglia data that is generated on several NCAR supercomputing
resources. It also includes a modified schema definition file that adds support
the the memory metrics that are generated on NCAR machines.

The dataset mapping file is installed alongside the default Open XDMoD mapping.
Enabling the mapping file requires a simple change to the resources
configuration file.

## Enabling the mapping

Edit the resources configuration file `/etc/xdmod/supremm_resources.json` (or
use the supremm-setup script to do this) and set the dataset mapping
`datasetmap` for each machine to the `ganglia-pcp` mapping.

    {
        "resource": "yellowstone",
        ...
        "datasetmap": "ganglia-pcp",
        ...
    }

The `ganglia-pcp` mapping routines need to know the number of processors per compute node. This value should be set in the 
`hardware` section of the resources configuration file `/etc/xdmod/supremm_resources.json`

    {
        "resource": "yellowstone",
        ...
        "hardware": {
            ...
            "ppn": 16
        }
    }

## Switching schema files

Edit the main SUPReMM configuration file `/etc/xdmod/portal_settings.d/supremm.ini` and
change the `supremm-general.schema_file` parameter to `etl.schema.ncar.js`

    ...
    [supremm-general]
    ...
    schema_file = "etl.schema.ncar.js"
    ...

After making this change it is necessary to run a script that updates the installed system files:

    cd /usr/share/xdmod/etl/js
    node etl.cli.js -a

