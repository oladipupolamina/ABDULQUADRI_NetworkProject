# ABDULQUADRI_NetworkProject
# 1. PROJECT OVERVIEW
This project involves designing and implementing a segmented network for three departments: Students, Teachers, and Admin. The network requires security enforcement using Access Control Lists (ACLs) to restrict what each group can access, especially the students’ subnet.
The goals are to:
-Ensure proper network segmentation using VLANs.
-Implement inter-VLAN routing using a router-on-a-stick design.
-Enforce security rules using ACLs.
-Test connectivity to confirm the ACLs work as intended.



# 2. REQUIREMENTS (GIVEN CONDITIONS)
 | VLAN  | Department | Network        | Devices                         |
|-------|------------|----------------|---------------------------------|
| 10    | Teachers   | 172.16.10.0/24 | 2 PCs                           |
| 20    | Students   | 172.16.20.0/24 | 2 Laptops and PCs               |
| 30    | Admin      | 172.16.30.0/24 | 1 PC & 1 Server (HTTPS, HTTP, FTP only) |

# FIREWALL/ACL RULES REQUIRED
# STUDENTS
The students can access only the Admin server on HTTP (80) & HTTPS (443) but cannot access the Admin PC and Teacher PCs. The student also cannot use any other ports (social media, games, etc.).
# TEACHERS
The teachers have full access to all departments.
# ADMIN
They have full access everywhere. The server only accepts HTTP, HTTPS, and FTP



# 3. NETWORK PLANNING
# Why VLAN Segmentation?
-Prevents broadcast storms.
-Provides departmental isolation.
-Improves security.
-Makes applying ACLs much easier since each department is in its own subnet.

# Why Router-on-a-Stick?
-Only one router interface was available.
-Sub-interfaces allow the router to route between VLANs.
-Efficient and standard in Cisco labs.

# Why ACLs on Router Sub-Interfaces?
-ACLs applied inbound on sub-interfaces filter packets as they leave each department, which ensures:
-Student restrictions apply before traffic enters the network core.
-Security policies remain simple and easy to maintain.
-Teachers and admins enjoy unrestricted access because nothing blocks them.


# **4. PROJECT PROCEDURE**
1. Draw your network (physical and logical).
2. Configure VLANs 10, 20, and 30 on your switch.
3. Assign PCs and laptops to the correct VLANs.
4. Configure trunking between switch and router (router-on-a-stick).
5. Set IP addresses according to the subnet table.
6. Configure inter-VLAN routing on router.
7. Write and apply ACLs (Standard ACLs): o Block Students from Teachers and Admin networks.
o Allow Students HTTP/HTTPS only to Admin Server.
o Allow Teachers and Admins full access.
o Restrict unnecessary ports for Students.
8. Test from each PC or laptop to ensure rules work.


# **5. TEST**
| Test Scenario                                  | Expected Result |
|-----------------------------------------------|----------------|
| Student PC → Teacher PC (any service)         | Blocked        |
| Student PC → Admin PC (any service)           | Blocked        |
| Student PC → Admin Server (HTTP/HTTPS)       | ✔ Allowed      |
| Student PC → Admin Server (FTP/other ports)  | Blocked        |
| Teacher PC → Student PC                       | ✔ Allowed      |
| Admin PC → Everywhere                          | ✔ Allowed      |
| Student browsing social media (wrong ports)  | Blocked        |
