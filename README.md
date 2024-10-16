# dictionary_collection

## About

- FreeRADIUS dictionary extracted from release 3.2.6 (2024-24-08), GNU GPL 2.0, https://github.com/FreeRADIUS/freeradius-server/releases
- GNU Radius dictionary extracted from release 1.6.1 (2008-12-17), GNU GPL 3.0, https://www.gnu.org/software/radius/

## Notes about DHCP Option82 injected by RouterOS bridge

- Configuration (RouterOS v7.9.2)
```
/ip dhcp-server set <bridge> address-pool=static-only
/ip dhcp-server config set radius-password=same-as-user|empty
/interface bridge set <bridge> dhcp-snooping=yes add-dhcp-option82=yes
```

- RouterOS sends DHCP Option82 values (Agent-Remote-Id, Agent-Circuit-Id, ADSL-Agent-Remote-Id, ADSL-Agent-Circuit-Id) as string not as octets. However, these AVPs are defined as octets in dictionaries (dictionary.rfc4679, dictionary.ericsson.ab).
- You can rewrite data type for these AVP in these dictionaries (octets > string) if you use only RouterOS NAS devices.
- Or you can use dictionaries as they are and convert the hexadecimal values to the string if you get a message with Option82 from RouterOS.
- Hexadecimal octets to ASCII: `echo "hexadecimal" | xxd -r -p`