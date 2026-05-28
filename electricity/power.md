# Shutting Down Electricity

## PDUs


- 192.168.100.50    pdu0                    colibri-pdu0 ibbootbar
- 192.168.100.51    pdu1                    colibri-pdu1 ibootpdu
- 192.168.100.52    pdu2                    colibri-pdu2 ibootpdu
- 192.168.100.53    sparepdu                colibri-sparepdu ibootpdu

## Connections:

- pdu0
  1. instrument
  2. nas
  3. marsvom2
  4. qnap-prod
  5. qnap-spare
  6. marmex
  7. marmex
  8. astelco-minipc|
- pdu1
  1. close-electronics
  2. close-electronics-spare
  3. blue-service-cabinet
  4. red-service-cabinet
  5.
  6.
  7.
  8.
- pdu2
  1. blue
  2. red
  3. host0
  4. plc-computer
  5. host1
  6. host2
  7. host3
  8. host3

## Notes

- host0 contains the access computer and so should be shut down last.
- qnap-prod and qnap-spare do not automatically come up
- control currently runs on host1

