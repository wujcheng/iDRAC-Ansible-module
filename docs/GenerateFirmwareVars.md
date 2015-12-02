# GenerateFirmwareVars

## Synopsis

Used to generate the firmware.yml file.

## Requirements

* [Dell WSMan Client API Python](https://github.com/hbeatty/dell-wsman-client-api-python)
* wsmancli and libwsman1 from [OpenWSMAN](https://openwsman.github.io/)
  * I would like to get rid of this dependency (for various reasons) by enhancing the Dell WSMan Client API Python with a new transport.
  * I know it works with these versions of Openwsman. Success may vary with other versions.
    * wsmancli (2.3.2-54.5) from Openwsman
    * libwsman1 (2.4.15-148.1) from Openwsman

## Options

| parameter     | required | default | choices   | comments                                  |
| ---------     | -------- | ------- | -------   | --------                                  |
| username      | yes      | none    |           | A user that has admin access to the iDRAC |
| password      | yes      | none    |           | Password of the above user                |
| hostname      | yes      | none    |           | Hostname or IP of the iDRAC               |
| name          | yes      | none    |           | This command is 'GenerateFirmwareVars'    |
| firmware_file | no       | none    |           | Current firmware.yml file to merge        |
| debug         | no       | none    |           | Turn on debug logging. This will also leave any xml files that might be generated. |

## Examples

```
- name: Generate Firmware Vars
  local_action: idrac username={{lom_user}} password={{lom_pass}}
    hostname={{lom_hostname}} name="GenerateFirmwareVars"
    firmware_file="group_vars/all/firmware.yml"
```

## Return Values

  * changed:
    * Desciption: Whether or not changes were made.
    * Type: bool
    * Values: true/false
  * failed:
    * Description: Whether or not the job creation was successful
    * Type: bool
    * Values: true/false
  * msg:
    * Description: A hopefully helpful message
    * Type: string

## Notes

* [idrac-roles/os-install](https://github.com/hbeatty/idrac-roles/tree/master/os-install)