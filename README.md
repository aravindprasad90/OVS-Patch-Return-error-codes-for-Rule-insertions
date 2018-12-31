# OVS-Patch-Return-error-codes-for-Rule-insertions
OVS Patch - Return error codes for Rule insertions

Currently, rule_insert() API does not have return value. There are some possible
scenarios where rule insertions can fail at run-time even though the static
checks during rule_construct() had passed previously.
Some possible scenarios for failure of rule insertions:
**) Rule insertions can fail dynamically in Hybrid mode (both Openflow and
Normal switch functioning coexist) where the CAM space could get suddenly
filled up by Normal switch functioning and Openflow gets devoid of
available space.
**) Some deployments could have separate independent layers for HW rule
insertions and application layer to interact with OVS. HW layer
could face any dynamic issue during rule handling which application could
not have predicted/captured in rule-construction phase.
Rule-insert errors for bundles are handled too in this pull-request.
