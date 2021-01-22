# Charts

Dumping ground for various Helm Charts

## To-Do

- Consolidate all peoplesoft-related kubernetes helm charts under a single project
- Deprecate consul and vault charts in favor of the official hashcorp variants
  * https://github.com/hashicorp/consul-helm
  * https://github.com/hashicorp/vault-helm
- Enhance mssql-linux implementation
  * archive purging
  * sandbox image from registry
  * ha-ag
  * passwords from vault in addition to autogen
  * configurable pvc
  * add rancher-compatible chart questions
- Split ps-midtier into separate components
  * ps-webapp
  * ps-ib
  * ps-prcs

> WARNING: don't spend too much time on this - there's bigger fish to fry
