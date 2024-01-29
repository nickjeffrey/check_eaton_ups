# check_eaton_ups
Nagios check for Eaton / PowerWare UPS

# Requirements
perl and snmpget on nagios server, SNMP enabled on UPS network management card

# Configuration

You will need a section in the services.cfg file on the nagios server that looks similar to the following.
```
# Define a service to check the Eaton UPS
# Parameters are SNMP community name
 define service {
         use                             generic-service
         hostgroup_name                  all_eaton_ups
         service_description             Eaton UPS
         check_command                   check_eaton_ups!public
         }
```

You will need a section in the commands.cfg file on the nagios server that looks similar to the following.
```
 # 'check_eaton_ups' command definition
 # parameters are -H hostname -C snmp_community
 define command{
         command_name    check_eaton_ups
         command_line    $USER1$/check_eaton_ups -H $HOSTADDRESS$ -C $ARG1$
         }
```

Login to the web-based interface of the UPS network management card, click Settings, SNMP.  Activate SNMP, set community string.
<img src=images/ups_enable_snmp.png>

# Output
You will see output similar to the following:
```
Eaton UPS OK - Model:Eaton 9PX 3000, Power input source:primaryUtility, Battery capacity:100%, Load:27%, Runtime remaining is 165 minutes, Number of alarms:0 
```

