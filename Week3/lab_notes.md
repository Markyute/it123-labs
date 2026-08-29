\# IT 123 - Week 3 Lab Notes

\## User and Group Management in Ubuntu Server



\*\*Student:\*\* John Mark C. Idanan \& Catlyn L. Ruiz



\## Part 2 - User \& Group Management in Ubuntu



Created student2 with `sudo adduser student2`, using User@123 as the password

and leaving the optional fields blank.



Added a description to the account with: sudo usermod -c "Test account for Week 3 Lab" student2

Checked it applied correctly with `getent passwd student2`.



Created a group called labusers and added student2 to it:

sudo groupadd labusers

sudo usermod -aG labusers student2



Confirmed with `groups student2` that it now belongs to both its own default

group and labusers.



Then set up the shared folder:

sudo mkdir /labdata

sudo chown root:labusers /labdata

sudo chmod 770 /labdata



`ls -ld /labdata` showed `drwxrwx--- root labusers`, meaning only root and

labusers members can get in.



\## Part 3 - Verification



Switched to student2 with `su - student2` and tried accessing /labdata —

worked fine, could list the folder and create a file with `touch`.



Then went back to adminuser, ran `sudo chmod 750 /labdata` to drop the

group's write permission, and tried again as student2. This time `touch`

failed with "Permission denied," which is exactly what should happen once

write access is removed from the group.



\## Part 4 - Exercise (Faculty/Student scenario)



Repeated the same pattern for the exercise:

\- Created faculty2 and student4 the same way as student2.

\- Created two groups, facultygrp and studentgrp, and added each user to their

&#x20; respective group.

\- Created /facultydata (owned by root:facultygrp, chmod 770 — full read/write

&#x20; for the group) and /studentdata (owned by root:studentgrp, chmod 750 —

&#x20; read-only for the group, no write).



Tested both:

\- As faculty2: could list and write to /facultydata — worked as expected.

\- As student4: could list /studentdata (read works), but `touch` failed with

&#x20; "Permission denied" — confirming read-only access.



\## Summary



| User      | Group       | Directory     | Permission | Result                              |

|-----------|-------------|---------------|------------|--------------------------------------|

| student2  | labusers    | /labdata      | 770 → 750  | Write allowed, then denied after chmod |

| faculty2  | facultygrp  | /facultydata  | 770        | Read/write allowed                   |

| student4  | studentgrp  | /studentdata  | 750        | Read allowed, write denied           |



\## Reflection



This one made the difference between 770 and 750 really concrete — same

folder, same group, but changing one digit in chmod completely changed

whether writing was allowed. Doing the faculty/student exercise right after

the guided part helped since it was basically the same steps again, just

with different names, so it reinforced the order you need to do things in:

create the user, create the group, add the user to the group, then set

ownership and permissions on the folder.



