Below are real-world, **scenario-based EC2 questions** with **clear explanation, examples, and step-by-step actions**. These are written the way interviewers expect you to think in production.

---

## 1️⃣ EC2 Root Disk is 100% Full – Fix Without Downtime

### Scenario
Your production EC2 is running, but the root volume (`/`) is completely full. Stopping the instance will cause downtime.

### Approach
You **extend the root EBS volume online** and grow the filesystem.

### Steps
1. Identify root volume
   ```bash
   df -h /
   lsblk
   ```
2. Increase EBS volume size from AWS Console (no reboot needed)
3. Check new size
   ```bash
   lsblk
   ```
4. Extend partition (if needed)
   ```bash
   growpart /dev/xvda 1
   ```
5. Extend filesystem
   - **EXT4**
     ```bash
     resize2fs /dev/xvda1
     ```
   - **XFS**
     ```bash
     xfs_growfs /
     ```

### Result
✔ Disk expanded
✔ No downtime
✔ Application continues running

---

## 2️⃣ Application Needs More Storage (EC2 is Running)

### Scenario
App logs or uploads are growing, but EC2 is already running.

### Best Practice
**Attach a new EBS data volume instead of touching root.**

### Steps
1. Create new EBS volume
2. Attach to running EC2
3. Format and mount
   ```bash
   mkfs.ext4 /dev/xvdf
   mkdir /data
   mount /dev/xvdf /data
   ```
4. Make it persistent
   ```bash
   echo '/dev/xvdf /data ext4 defaults 0 2' >> /etc/fstab
   ```

### Result
✔ No downtime
✔ Clean separation of OS and data

---

## 3️⃣ Ensure Data Is Not Deleted When EC2 Is Terminated

### Key Setting
EBS **Delete on Termination = False**

### Steps
1. Go to EC2 → Storage → Volume
2. Disable **Delete on termination**

### Additional Protection
- Take **EBS snapshots** regularly
- Store backups in **S3**

---

## 4️⃣ Application Slow Due to High Disk I/O

### Investigation
```bash
iostat -x
lsblk
top
```

### Common Fixes
- Change volume type: **gp2 → gp3 / io1**
- Increase IOPS / throughput
- Separate logs and DB data onto different volumes
- Enable **EBS-optimized instance**

### Example
Move heavy logs to a separate gp3 volume.

---

## 5️⃣ EC2 Running but SSH Not Accessible

### Step-by-Step Debugging
1. Check Security Group (port 22 allowed)
2. Check NACL rules
3. Verify correct key pair
4. Instance status checks (2/2 passed?)
5. Disk full? (SSH can fail)
6. Use **EC2 Instance Connect / SSM Session Manager**

### Last Option
Detach root volume → attach to rescue EC2 → fix config → reattach

---

## 6️⃣ EC2 Deleted Accidentally – How to Recover Data

### Possible Recovery Paths
- Root volume snapshot exists → restore
- Data volume detached → attach to new EC2

### Best Practice
- Automated snapshots
- Infrastructure as Code (Terraform/CloudFormation)

---

## 7️⃣ Same Data Needed in Another AZ

### Options
- Take EBS snapshot → restore in another AZ
- Use **EFS** (AZ-independent)
- Replicate data to **S3**

### Recommended
✔ **EFS** for shared data
✔ **S3** for backups

---

## 8️⃣ Two EC2 Instances Need Same Data Simultaneously

### Wrong Design ❌
- Sharing EBS (not allowed)

### Correct Designs ✅
- **Amazon EFS** (POSIX, shared filesystem)
- **S3** (object storage)

### Example
Web servers sharing uploads → **EFS**

---

## 9️⃣ High AWS Bill Due to EBS Usage

### Cost Optimization Steps
- Delete unused volumes
- Remove old snapshots
- Move gp2 → gp3
- Right-size IOPS
- Enable lifecycle policies

### Example
Switch gp2 → gp3 → save ~20–30%

---

## 🔟 Traffic Suddenly Increases 10× – Handling Scale & Stability

### Immediate Actions
- Enable **Auto Scaling Group**
- Use **Application Load Balancer**
- Scale database (read replicas)

### Long-Term Design
- Stateless EC2
- Cache with Redis
- Use CDN

### Result
✔ No crash
✔ Controlled scaling
✔ Cost-efficient handling

---

## 💡 Interview Tip
Always explain:
1. **Impact**
2. **Root cause**
3. **Fix**
4. **Prevention**

If you want, I can convert this into:
- 📌 LinkedIn post
- 📄 Interview-ready PDF
- 🧠 Mock interview answers

