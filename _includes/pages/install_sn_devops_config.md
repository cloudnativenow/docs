### Install ServiceNow DevOps Config

ServiceNow DevOps Config helps Cloud Native Teams define advanced validation rules for comparing *configuration* changes against defined baselines and preventing unauthorised changes to deployment environments. Use the built-in Change Approval Workflows to completely automate the change approval process. Installation is as folows:

1. Login to your SN Instance as Administrator

1. Navigate to the **System Definition > Plugins** and install or activate the following plugins:

   | Plugin Name                                   | Plugin ID              |
   | --------------------------------------------- | ---------------------- |
   | DevOps Config V1.0.3                          | `sn_devops_config`     |
   | DevOps Config Insights V1.0.3                 | `sn_devops_config_i`   |
   | DevOps Config Policy Content Pack V1.0.3      | `sn_devops_config_p`   |
   | DevOps Config Exporter Content Pack V1.0.3    | `sn_devops_config_e`   |
   | Configuration Data Management V1.0.0          | `sn_cdm`               |
   | Context Menu Component V1.0.0                 | `sn_cdm_ctx_menu`      |
   | Policy as Code Engine V1.0.0                  | `sn_pace`              |