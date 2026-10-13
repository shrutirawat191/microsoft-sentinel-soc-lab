### Inbound Authentication from Public IP

### Overview

This Microsoft Sentinel lab demonstrates how to identify authentication attempts originating from public IP addresses using Microsoft Sentinel and Kusto Query Language (KQL).

### Objective

Detect successful and failed authentication events associated with public IP addresses and enrich the results with device information.

### Risk

Devices exposed to the public internet are more prone to exploitation. Monitoring authentication attempts from public IP addresses can help identify potentially suspicious access activity.

### Create scheduled rule

<img width="975" height="635" alt="image" src="https://github.com/user-attachments/assets/46f7d8ff-9872-4bef-9b9f-80dad61aac45" />

**KQL query**

                                                    let AllowedEntpoints = pack_array('devicename');
                                                    SecurityEvent
                                                    | where EventID in ('4625', '4624')
                                                    | where Computer !in(AllowedEntpoints)
                                                    | where not(ipv4_is_private(IpAddress))
                                                    | summarize arg_min(TimeGenerated, *) by Computer
                                                    | lookup kind=leftouter (DeviceInfo
                                                       | summarize arg_max(TimeGenerated, *) by DeviceId
                                                       | project DeviceName = toupper(DeviceName), DeviceType, PublicIP, ExposureLevel, MachineGroup) on $left.Computer == $right.DeviceName

<img width="975" height="575" alt="image" src="https://github.com/user-attachments/assets/ee5a5c84-00bb-4a0e-9734-24a732dca217" />

<img width="975" height="439" alt="image" src="https://github.com/user-attachments/assets/4d328085-37ce-4f2b-9994-e4ecb5f9af99" />

 ### Testing

login and change following settings

<img width="975" height="718" alt="image" src="https://github.com/user-attachments/assets/d6a9f2e8-54ae-451a-bfa7-1f53d691daca" />

Rule was triggered and incident was generated.

<img width="975" height="527" alt="image" src="https://github.com/user-attachments/assets/046105c7-e36c-4f95-b667-08fbaf3f253c" />

<img width="970" height="791" alt="image" src="https://github.com/user-attachments/assets/2813074a-100d-4703-932a-9833ec762ca3" />

