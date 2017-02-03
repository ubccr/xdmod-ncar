# xdmod-ncar

The NCAR module delivers a customized SUPReMM realm dataset mapping file that
supports the Ganglia data that is generated on several NCAR supercomputing
resources. 

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

