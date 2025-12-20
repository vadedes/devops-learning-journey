# DevOps Learning Journey 🚀

A hands-on documentation of my transition from web development to DevOps engineering. This repository tracks my practical learning experiences, focusing on real-world implementations rather than just theory.

**Learning Philosophy**: 80/20 approach (80% hands-on practice, 20% theory)

---

## 📚 Course Progress

**Current Focus**: [KodeKloud - DevOps Prerequisites Course](https://kodekloud.com/)
- ✅ Introduction Module
- 🔄 Linux Basics (In Progress)

---

## 🛠️ Learning Modules

### Module 1: Linux & SSH Fundamentals

**Completion Date**: [Current]  
**Practice Environment**: DigitalOcean Droplet  
**Hands-on Hours**: ~8 hours

#### Overview
Rather than just watching tutorials, I immediately set up a live practice environment using a DigitalOcean droplet. This allowed me to learn SSH authentication, user management, and security hardening through real implementation.

#### What I Built
- Multi-user SSH authentication system
- Configured SSH key-based authentication for 7 different users
- Implemented SSH hardening best practices
- Practiced user lifecycle management (creation, access control, offboarding)

#### Key Concepts Mastered

**1. SSH Key Authentication**

Understanding the fundamentals of how SSH keys work:

- **Key Pairs**: SSH uses asymmetric encryption with two keys
  - **Private Key**: Stored securely on local machine (`~/.ssh/id_rsa` or `id_ed25519`)
  - **Public Key**: Placed on remote servers (`~/.ssh/authorized_keys`)
  - Never share your private key - it's like your password, but better

- **Authentication Flow**: 
  1. Client sends public key to server
  2. Server challenges client to prove it has the private key
  3. Client responds with cryptographic proof
  4. Connection established without password

**2. Managing Multiple SSH Identities**

Learned to manage different keys for different users/purposes:

```bash
# Generate key for admin access
ssh-keygen -t ed25519 -C "do_root_key"
# Save as: ~/.ssh/id_do_root

# Generate key for regular user access
ssh-keygen -t ed25519 -C "do_alice_key"
# Save as: ~/.ssh/id_do_alice
```

**3. SSH Configuration for Convenience**

Created `~/.ssh/config` to manage multiple connections efficiently:

```text
Host do-root
    HostName your_droplet_ip
    User root
    IdentityFile ~/.ssh/id_do_root

Host do-alice
    HostName your_droplet_ip
    User alice
    IdentityFile ~/.ssh/id_do_alice
```

Now I can simply use: `ssh do-root` or `ssh do-alice`

#### Practical Implementation

**Setting Up Root Access**
```bash
# Copy public key to root user
ssh-copy-id -i ~/.ssh/id_do_root.pub root@your_droplet_ip

# Test connection
ssh -i ~/.ssh/id_do_root root@your_droplet_ip
```

**Creating and Configuring New Users**
```bash
# On the droplet as root
adduser alice
usermod -aG sudo alice

# Set up SSH for alice
mkdir -p /home/alice/.ssh
nano /home/alice/.ssh/authorized_keys  # Add alice's public key
chown -R alice:alice /home/alice/.ssh
chmod 700 /home/alice/.ssh
chmod 600 /home/alice/.ssh/authorized_keys
```

**SSH Hardening (Security Best Practices)**
```bash
# Edit SSH configuration
sudo nano /etc/ssh/sshd_config

# Key security settings
PermitRootLogin prohibit-password
PasswordAuthentication no

# Restart SSH service
sudo systemctl restart ssh
```

**User Offboarding (Access Revocation)**
```bash
# Lock user account
sudo passwd -l alice

# Or remove SSH key access
sudo nano /home/alice/.ssh/authorized_keys  # Remove key

# Complete removal (use with caution)
sudo userdel -r alice
```

#### Commands Practiced to Build Muscle Memory

**User Management**:
- `adduser` - Create new user accounts
- `usermod -aG sudo` - Add users to sudo group
- `passwd -l` - Lock user accounts
- `userdel -r` - Delete users and their home directories

**SSH Operations**:
- `ssh-keygen` - Generate SSH key pairs
- `ssh-copy-id` - Copy public keys to remote servers
- `ssh -i` - Connect using specific identity file
- `chmod` - Set correct permissions (700 for directories, 600 for keys)
- `chown` - Change file ownership

**File Management**:
- `mkdir -p` - Create directories with parent directories
- `nano` / `vim` - Edit configuration files
- `cat` - View file contents
- `chmod` - Modify file permissions

#### Real-World DevOps Skills Developed

✅ **Security**: Disabled password authentication, implemented key-based auth only  
✅ **Access Control**: Practiced principle of least privilege with sudo access  
✅ **User Lifecycle Management**: Created, configured, and offboarded users  
✅ **Configuration Management**: Maintained consistent SSH configuration  
✅ **Troubleshooting**: Debugged permission issues and connection problems  
✅ **Documentation**: Learned to document processes for team use  

#### Lessons Learned

1. **Repetition Builds Mastery**: Manually creating 7 users forced me to internalize the commands and understand the "why" behind each step, not just the "how"

2. **Permissions Matter**: Many initial connection issues stemmed from incorrect file permissions - taught me the importance of security defaults

3. **Configuration Files Are Powerful**: The `~/.ssh/config` file dramatically improved my workflow - a small optimization that saves time daily

4. **Security by Default**: Learned that DevOps isn't just about making things work, but making them work *securely* from the start

#### Next Steps for This Module

- [ ] Practice SSH tunneling and port forwarding
- [ ] Set up SSH bastion host (jump server)
- [ ] Implement fail2ban for SSH protection
- [ ] Practice SSH debugging with `-v` flags

---

## 📊 Learning Stats

- **Total Learning Hours**: 8+ hours (and counting)
- **Active Practice Labs**: 1 (DigitalOcean droplet)
- **Commands Mastered**: 15+
- **Real Scenarios Completed**: 3 (key generation, user management, SSH hardening)

---

## 🔄 What's Next?

**Upcoming Modules**:
- Linux file system and permissions
- Package management (apt/yum)
- Process management and system monitoring
- Shell scripting basics

**Long-term Goals**:
- Docker & Kubernetes
- AWS Cloud Services
- Terraform (Infrastructure as Code)
- CI/CD Pipelines
- AWS Solutions Architect Associate certification
- CKA (Certified Kubernetes Administrator)

---

## 💡 Learning Approach

**My 3-Step Process**:
1. **Watch & Understand**: Complete course modules to grasp concepts
2. **Build Immediately**: Set up practice lab and implement what I learned
3. **Repeat & Refine**: Practice until commands become muscle memory

**Why This Works for Me**: Coming from a web development background, I learn best by breaking things and fixing them. Theory without practice doesn't stick.

---

## 📝 Notes

- All practice is done on real infrastructure (DigitalOcean droplet), not just local VMs
- Every command listed here has been typed manually multiple times
- Mistakes and troubleshooting are part of the learning process - they're documented as lessons learned

---

## 🤝 Connect With Me

This is a living document that will be updated as I progress through my DevOps journey. Feel free to reach out if you have suggestions or want to discuss any of these topics!

**Last Updated**: [Add Date]

---

*This repository serves as both a learning log and a technical reference for my DevOps skills development.*