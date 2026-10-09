# AWS Security using Security Groups and NACL 

AWS (Amazon Web Services) provides multiple layers of security to protect resources and data within its cloud infrastructure. Two important components for network security in AWS are Security Groups and Network Access Control Lists (NACLs). Let's explore how each of them works:

    Security Groups:
        Security Groups act as virtual firewalls for Amazon EC2 instances (virtual servers) at the instance level. They control inbound and outbound traffic by allowing or denying specific protocols, ports, and IP addresses.
        Each EC2 instance can be associated with one or more security groups, and each security group consists of inbound and outbound rules.
        Inbound rules determine the traffic that is allowed to reach the EC2 instance, whereas outbound rules control the traffic leaving the instance.
        Security Groups can be configured using IP addresses, CIDR blocks, security group IDs, or DNS names to specify the source or destination of the traffic.
        They operate at the instance level and evaluate the rules before allowing traffic to reach the instance.
        Security Groups are stateful, meaning that if an inbound rule allows traffic, the corresponding outbound traffic is automatically allowed, and vice versa.
        Changes made to security group rules take effect immediately.

    Network Access Control Lists (NACLs):
        NACLs are an additional layer of security that operates at the subnet level. They act as stateless traffic filters for inbound and outbound traffic at the subnet boundary.
        Unlike Security Groups, NACLs are associated with subnets, and each subnet can have only one NACL. However, multiple subnets can share the same NACL.
        NACLs consist of a numbered list of rules (numbered in ascending order) that are evaluated in order from lowest to highest.
        Each rule in the NACL includes a rule number, protocol, rule action (allow or deny), source or destination IP address range, port range, and ICMP (Internet Control Message Protocol) type.
        NACL rules can be configured to allow or deny specific types of traffic based on the defined criteria.
        They are stateless, which means that if an inbound rule allows traffic, the corresponding outbound traffic must be explicitly allowed using a separate outbound rule.
        Changes made to NACL rules may take some time to propagate to all the resources using the associated subnet.

## Project Implemented in the video


![Screenshot 2023-06-29 at 12 14 32 AM](https://github.com/iam-veeramalla/aws-devops-zero-to-hero/assets/43399466/30bbc9e8-6502-438b-8adf-ece8b81edce9)



# Learn-it-Simple

# AWS Security Groups vs. Network ACLs (NACLs) - Quick Cheat Sheet

---

## 1. The Ultimate Analogy (The Bank)
* **Security Group (The Room Guard):** Stands right outside an individual server door (EC2 instance). It knows who you are and is **stateful**—meaning if it lets you *in*, it automatically remembers you and lets you back *out*.
* **NACL (The Building Gate):** Stands at the outer perimeter gate (Subnet boundary). It checks traffic in bulk and is **stateless**—meaning if it lets you *in*, you must explicitly configure a separate outbound rule to let it *out*.

---

## 2. Security Groups (Instance-Level Firewall)
* **Where it works:** Directly on the individual EC2 server (instance level).
* **Scope:** Each instance can be associated with one or more security groups.
* **State (Crucial for Interviews):** **Stateful**. If an inbound rule allows traffic *in*, the response traffic is automatically allowed *out* (no outbound rule needed).
* **Rule Evaluation:** Evaluates *all* rules together before deciding whether to allow traffic.
* **Changes:** Take effect **immediately**.

---

## 3. Network ACLs / NACLs (Subnet-Level Firewall)
* **Where it works:** At the entire subnet boundary (protects all servers inside that subnet).
* **Scope:** Associated with subnets (one NACL per subnet, though multiple subnets can share one).
* **State (Crucial for Interviews):** **Stateless**. If an inbound rule allows traffic *in*, you must manually create a separate outbound rule to allow the response back *out*.
* **Rule Evaluation:** Evaluated in a strict **numerical order** (lowest number to highest number; stops at the first rule that matches).
* **Changes:** Can take some time to propagate.

---

## 4. Quick Comparison Table

| Feature | Security Groups (SGs) | Network ACLs (NACLs) |
| :--- | :--- | :--- |
| **Scope** | Instance level (EC2) | Subnet level |
| **Stateful / Stateless** | **Stateful** (remembers incoming/outgoing) | **Stateless** (requires separate inbound/outbound rules) |
| **Rule Evaluation** | Evaluates all rules together | Evaluates rules in numerical order |
| **Default Action** | Deny all inbound, allow all outbound | Allow all inbound and outbound |
| **Speed of Changes** | Takes effect immediately | Can take time to propagate |

