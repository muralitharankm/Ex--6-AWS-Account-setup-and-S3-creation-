# CLOUD STORAGE CREATION (S3) AND LAUNCHING AN (EC2) INSTANCE IN AWS
## NAME: Stephen raj Y
## REG NO: 212223230217

## Aim

To create and configure an Amazon Elastic Block Store (EBS) volume, attach and mount it to an Amazon EC2 instance, create a snapshot backup, and restore the snapshot to a new EBS volume.

---

## Algorithm / Steps

1. Create a new Amazon EBS volume with a size of 1 GiB.
2. Select the same Availability Zone as the EC2 instance.
3. Attach the EBS volume to the EC2 instance using `/dev/sdb`.
4. Connect to the EC2 instance using AWS Systems Manager Session Manager.
5. Check the available storage using `df -h`.
6. Create an `ext3` file system on the EBS volume.
7. Create the `/mnt/data-store` directory.
8. Mount the EBS volume to `/mnt/data-store`.
9. Configure `/etc/fstab` for automatic mounting.
10. Verify that the EBS volume is successfully mounted.
11. Create `file.txt` inside the mounted EBS volume.
12. Verify the contents of the created file.
13. Create an EBS snapshot named `My Snapshot`.
14. Delete `file.txt` from the original EBS volume.
15. Create a new EBS volume from the snapshot.
16. Attach the restored volume to the EC2 instance using `/dev/sdc`.
17. Create the `/mnt/data-store2` directory.
18. Mount the restored volume to `/mnt/data-store2`.
19. Verify that `file.txt` has been successfully restored.

---

## Program

### 1. Check Available Storage

```bash
df -h
```

### 2. Create an ext3 File System

```bash
sudo mkfs -t ext3 /dev/sdb
```

### 3. Create a Mount Directory

```bash
sudo mkdir /mnt/data-store
```

### 4. Mount the EBS Volume

```bash
sudo mount /dev/sdb /mnt/data-store
```

### 5. Configure Automatic Mounting

```bash
echo "/dev/sdb   /mnt/data-store ext3 defaults,noatime 1 2" | sudo tee -a /etc/fstab
```

### 6. View the File System Configuration

```bash
cat /etc/fstab
```

### 7. Verify the Mounted Volume

```bash
df -h
```

### 8. Create a File in the EBS Volume

```bash
sudo sh -c "echo some text has been written > /mnt/data-store/file.txt"
```

### 9. Read the File

```bash
cat /mnt/data-store/file.txt
```

### 10. Delete the File

```bash
sudo rm /mnt/data-store/file.txt
```

### 11. Verify File Deletion

```bash
ls /mnt/data-store/
```

### 12. Create a Mount Directory for the Restored Volume

```bash
sudo mkdir /mnt/data-store2
```

### 13. Mount the Restored EBS Volume

```bash
sudo mount /dev/sdc /mnt/data-store2
```

### 14. Verify Snapshot Restoration

```bash
ls /mnt/data-store2/
```

Expected output:

```text
file.txt
```

---

## Outputs
<img width="1600" height="768" alt="WhatsApp Image 2026-08-03 at 12 24 26 PM" src="https://github.com/user-attachments/assets/aae4c762-b784-40d5-8b7b-037a88f2d738" />
<img width="1600" height="764" alt="WhatsApp Image 2026-08-03 at 12 24 26 PM (1)" src="https://github.com/user-attachments/assets/99bcecf6-ad32-44b7-8bde-3a558ab15b49" />
<img width="1875" height="595" alt="image" src="https://github.com/user-attachments/assets/e8b07536-dcc9-4fef-a7a3-1d34561eafcb" />
<img width="1871" height="707" alt="image" src="https://github.com/user-attachments/assets/792cba49-fa3e-4216-87c5-eef341e13b81" />
<img width="1917" height="606" alt="image" src="https://github.com/user-attachments/assets/1d5891cd-62e5-4617-a66a-bf16219c886a" />
<img width="1600" height="760" alt="WhatsApp Image 2026-08-03 at 12 24 26 PM (4)" src="https://github.com/user-attachments/assets/7f655a62-e10d-474a-a207-3855c9fddbe4" />
<img width="1918" height="930" alt="Screenshot 2026-07-28 085356" src="https://github.com/user-attachments/assets/2f9931e1-fb42-4081-bb52-3c139de21c27" />
<img width="1548" height="546" alt="Screenshot 2026-07-28 093318" src="https://github.com/user-attachments/assets/f6eae027-bb65-4f3e-bf37-09794ca56ff0" />






## Result
Thus, an Amazon EBS volume was successfully created and attached to an Amazon EC2 instance. The volume was formatted with an ext3 file system, mounted, and used for storing data. An EBS snapshot was successfully created as a backup, and a new EBS volume was restored from the snapshot. The previously deleted file.txt was successfully recovered, demonstrating the backup and restore functionality of Amazon EBS.
