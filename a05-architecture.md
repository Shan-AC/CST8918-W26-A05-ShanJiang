

##  Architecture Diagram 

```mermaid

graph TD
    %% External Traffic Input
    Internet([Internet]) --> PIP[Public IP: ShanJiang-pip]
    
    %% Firewall Security Boundary
    PIP --> NSG[Network Security Group: ShanJiang-nsg]
    
    subgraph NSG_Rules [NSG Inbound Rules]
        SSH[Port 22: Allow SSH]
        HTTP[Port 80: Allow HTTP]
    end
    NSG --> SSH
    NSG --> HTTP

    %% Virtual Network and Virtual Machine Boundary
    subgraph VNet [Virtual Network: ShanJiang-vnet 10.0.0.0/16]
        subgraph Subnet [Subnet: ShanJiang-subnet 10.0.1.0/24]
            NIC[Network Interface: ShanJiang-nic]
            
            subgraph VM_Instance [Virtual Machine Instance]
                VM[Ubuntu VM: ShanJiang-vm Standard_B2ats_v2]
                Apache[Apache2 Web Server]
            end
        end
    end

    %% Network Traffic Flow Binding
    SSH --> NIC
    HTTP --> NIC
    NIC --> VM
    VM --> Apache
    ```
