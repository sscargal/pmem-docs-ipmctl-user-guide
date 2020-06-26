# Security

Intel Optane persistent memory modules support data-at-rest security by encrypting the data stored in the persistent regions of the DIMM. The `ipmctl` utility provides commands to enable, disable, and manage the security features.

{% hint style="info" %}
**NOTE:** Security commands are subject to Operating System Vendor \(OSV\) support and will return "Not Supported." An exception is if the module is in Unlocked Security State, then transitioning to Disabled is permitted.
{% endhint %}

For further security information, refer to the [Managing NVDIMM Security](https://docs.pmem.io/ndctl-user-guide/managing-nvdimm-security) section of the NDCTL user guide.

