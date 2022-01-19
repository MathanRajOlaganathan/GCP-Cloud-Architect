- HostName/ProjectID/Image:Tag - gcr.io/projectname/helloworld:1
- KMS - key management services
- Blob Storage - Local SSD, Persistent Disks(Standard, SSD, Balanced)
- snapshots - point-in-time backups of pds
- cloud storage bucket name should be unique globally
  
**IAM**

- IAm member - who, roles - set of permissions, policy - bind member with role
- permissions are not directly assigned to member, only thro roles
- member can be user, serviceaccount, group/domain
-  <img src="/Users/matolaga/Mathan/Git/GCP/src/main/resources/IAM Policy.png" width="500" height="300">
-  <img src="/Users/matolaga/Mathan/Git/GCP/src/main/resources/PolicyTroubleShooter.png" width="500" height="300">
-  <img src="/Users/matolaga/Mathan/Git/GCP/src/main/resources/PolicyTrouble_result.png" width="500" height="300">
- use service accounts when an app needs to access any cloud resources.
- SA doesnt have password, they have pri/pub RSA key-pairs. Can't login via browsers.
- SA type - Default SA, User Managed(Recommended), Google-Manged(Used by GCP tp perform ops on user's behalf)
- use ACL if u need custom access to individual objects, use IAM for common permissions to all the objects in a bucket
- Signed url allows a user limited time access to your objects.
- Its sufficient either IAM or ACL allow access.