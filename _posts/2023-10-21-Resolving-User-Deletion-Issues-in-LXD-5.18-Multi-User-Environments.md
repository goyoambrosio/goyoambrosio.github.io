---
title: "Resolving User Deletion Issues in LXD 5.18 Multi-User Environments"
layout: # single
classes: wide
author_profile: # true
read_time: # true
comments: # true
share: # true
related: #true
excerpt: # Auto-generated page excerpt is added to the overlay text or can be overridden here.
excerpt_separator: # "<!--more-->"
header:
  overlay_color: "#000000" 
  overlay_filter: "0.6" # 1.0 Darkest
  overlay_image: "/assets/images/2023/10/LXD-multi-user.webp"
  caption: # ""
  image_description: "LXD multi-user environment"
  teaser: "/assets/images/2023/10/LXD-multi-user.webp"
  show_overlay_excerpt: # true
categories:
  - tutorial
tags: 
  - LXD
  - multi-user
  - Ubuntu
  - lxc
  - container
last_modified_at: 2023-10-21
---

LXD, the system container manager, has become a popular choice for many developers and sysadmins due to its lightweight nature and ease of use. However, like any software, it can sometimes present challenges. One such challenge that has been identified in LXD version 5.18, especially in multi-user environments, is the difficulty in properly deleting a user. This post will delve into this issue and provide a comprehensive solution.

## The Problem

In LXD 5.18 multi-user setups, when attempting to delete a user from the system, not all references to that user and their associated UID are removed. This lingering data can cause conflicts, especially if you try to recreate a user with the same name or if the system tries to reuse the UID for a new user.

## The Solution

To ensure a clean removal of a user and all their associated LXD resources, follow the steps below:

1. **Delete the User from the System**:
   - First, retrieve the user's UID with:
     ```bash
     DELUID = id <username>
     ```
   - Then, delete the user and their home directory:
     ```bash
     sudo deluser <username> --remove-home
     ```

2. **Clean Up LXD Resources**:
   - Switch to the user's LXD project (assuming each user has their own LXD project based on their UID):
     ```bash
     lxc project switch user-${DELUID}
     ```
   - Delete all instances (containers, VMs) associated with the user's project:
     ```bash
     lxc list
     lxc delete <instances> --force
     ```
   - Remove all images tied to that user:
     ```bash
     lxc image list
     lxc image delete <FINGERPRINT>
     ```
   - Finally, delete the user's LXD project:
     ```bash
     lxc project delete user-${DELUID}
     ```

3. **Remove LXD Network Resources**:
   - If each user has their own LXD bridge network, remove it:
     ```bash
     lxc network list
     lxc network delete lxdbr-${DELUID}
     ```

4. **Revoke Trust**:
   - List all trusted certificates:
     ```bash
     lxc config trust list
     ```
   - Delete the certificate associated with the user:
     ```bash
     lxc config trust delete lxd-user-${DELUID}
     ```

5. **Clean Up User's LXD Configuration**:
   - Ensure all user-specific LXD configurations and data are removed:
     ```bash
     sudo ls -al /var/snap/lxd/common/lxd-user/users
     sudo rm -rf /var/snap/lxd/common/lxd-user/users/${DELUID}
     ```

6. **Add a New User**:
   - With all references to the old user cleaned up, you can now safely add a new user to the system:
     ```bash
     sudo adduser <new_user>
     sudo adduser <new_user> users
     ```

## Conclusion

While LXD offers a powerful platform for container management, it's essential to be aware of potential pitfalls and know how to navigate them. This guide provides a solution to a specific issue in LXD 5.18, ensuring a smooth user management experience in multi-user environments. Always remember to backup any crucial data before performing such operations and double-check each command to avoid unintended data loss.


