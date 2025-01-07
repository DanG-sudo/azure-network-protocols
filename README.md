<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

<p align="left">

 1. Understanding Network Security Groups (NSGs)

Define NSGs: Clearly explain that NSGs are used in Azure to control inbound and outbound traffic to and from Azure resources (like VMs).
Explain Scope of NSGs: Describe how NSGs can be applied to:

    Subnets: Securing multiple VMs within a subnet.
    Network Interfaces (NICs): Securing specific VMs within the same subnet.

    Rules Overview:
        Inbound Rules: Control incoming traffic to a resource.
        Outbound Rules: Control outgoing traffic from a resource.
        Priority-Based Rules: Lower priority numbers have higher precedence.
        Default Rules: Mention Azure’s default rules that allow/deny specific traffic (e.g., allow VNet-to-VNet communication).
2. NSG Configuration Checklist
 
a. Create and Associate NSGs

Create NSG in Azure Portal:

    Navigate to Networking > Network Security Groups > + Create.
    Define a name (e.g., VM-Security-NSG) and associate it with a resource group and region.

    Associate NSG to Subnet or NIC:
        Attach the NSG to the target subnet for broader scope or to the VM’s NIC for granular control.

  b. Configure Custom Rules

Inbound Rules:

    Define application-specific rules (e.g., HTTP, RDP, SSH).
    
  ![view-security-rule-details](https://github.com/user-attachments/assets/0e38022e-b96d-4990-8f1b-2d3d9ad7eb65)

    Example: Allow HTTP traffic on TCP port 80 from a specific IP range.

Outbound Rules:

    Restrict unnecessary outbound traffic to reduce attack surface.
    Example: Block outbound internet access unless necessary.

    Security Best Practices:
        Deny all traffic by default and allow only necessary traffic.
        Use Service Tags (e.g., AzureLoadBalancer, Internet) to simplify rules.
        Use Application Security Groups (ASGs) for logical grouping.

3. Inspect Traffic Between Azure Virtual Machines
a. Set Up NSG Rules for Testing

Create Allow Rule for Testing:

    Allow traffic between VMs using their private IPs.
    Example: Allow TCP traffic on port 8080 for testing a web application.

    Test Deny Rules:
        Deny traffic for specific ports (e.g., block RDP on port 3389 for certain IP ranges).

b. Use Tools to Inspect Traffic

Azure Network Watcher:

![cm-reason-of-failure](https://github.com/user-attachments/assets/a0704ec3-16ee-4a8d-a7c4-c666b1595963)

    Enable Network Watcher in the target region.
    Use the Connection Troubleshoot tool to test connectivity between VMs.

Packet Capture:
![portal-search](https://github.com/user-attachments/assets/26fb8b04-7dde-4095-b9f6-8ea57f1047aa)

    Set up packet capture in Network Watcher to analyze traffic patterns and diagnose issues.
    Download and inspect the capture file using tools like Wireshark.

![packet-capture](https://github.com/user-attachments/assets/be6191ac-f6be-43f9-b601-6065c7f65d16)


    Network Performance Monitor (NPM):
        Monitor latency, packet loss, and network health.
        Set up NPM to visualize traffic flow and identify bottlenecks.

4. Demonstrating NSG Rules and Traffic Analysis


    ![image](https://github.com/user-attachments/assets/aa4082cf-4a3f-4bfd-ab5c-0c829fb1fbe0)


b. Traffic Inspection Example

![image](https://www.varonis.com/hubfs/Imported_Blog_Media/Screen-Shot-2021-07-05-at-4_58_25-PM-1024x659.png)

    

c. Real-World Scenarios

Scenario 1: Allow secure SSH/RDP access to VMs from an on-premises IP range.
Scenario 2: Deny all inbound traffic except HTTP/HTTPS for a web application.

    Scenario 3: Block outbound traffic to the internet except for specific services like Azure Storage.

5. Highlighting Security Best Practices

Use Least Privilege Principles:

    Restrict traffic to only what is required.

Regularly Audit NSGs:

    Check for unused rules and overly permissive configurations.

Enable Azure Monitor and Log Analytics:

    Set up alerts for unauthorized or suspicious traffic patterns.

Implement Zero Trust Networking:

    Combine NSGs with other Azure security features like Azure Firewall or DDoS Protection.

</p>
