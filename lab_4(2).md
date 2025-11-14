# Lab_4 (File Back and Automation)

## 1.⁠ ⁠Backup.sh Script

Create a new file named backup.sh inside your project folder:
<img width="734" height="627" alt="Screenshot from 2025-11-14 14-59-40" src="https://github.com/user-attachments/assets/da041487-37ce-4a20-94e8-cbb665c44508" />

## 2. Make Script Executable

Run the following command once:

```bash
chmod +x Backup.sh
```

## 3. Testing the script

### 1. Create some samples .txt files:
<img width="768" height="98" alt="Screenshot from 2025-11-14 14-57-16" src="https://github.com/user-attachments/assets/1ca59625-7597-4fb6-87eb-1ca619c74822" />

### 2. Run the script:
./backup.sh
<img width="743" height="54" alt="Screenshot from 2025-11-14 14-58-05" src="https://github.com/user-attachments/assets/63a5b4b3-3d06-4a89-ac80-ca9403da794e" />



# LAB 5 (File backup and automation)
## Objective
Automate the backup of ⁠ .txt ⁠ files into a ⁠ backup/ ⁠ folder with timestamps in filenames.

---

## Script Explanation

1.⁠ ⁠⁠ mkdir -p backup ⁠  
   Creates a folder named ⁠ backup ⁠ if it does not exist.

2.⁠ ⁠⁠ timestamp=$(date +"%Y%m%d_%H%M%S") ⁠  
   Generates a timestamp (format: YYYYMMDD_HHMMSS).

3.⁠ ⁠⁠ for file in *.txt; do ... done ⁠  
   Loops through all ⁠ .txt ⁠ files in the current directory.

4.⁠ ⁠⁠ basename "$file" .txt ⁠  
   Extracts the file name without extension.

5.⁠ ⁠⁠ cp "$file" "backup/${filename}_$timestamp.txt" ⁠  
   Copies the file into ⁠ backup/ ⁠ with the timestamp appended.

---

### Input
Created two ⁠ .txt ⁠ files:

file1.txt
file2.txt

### Command
./Backup.sh

### Output
<img width="743" height="54" alt="Screenshot from 2025-11-14 14-58-52" src="https://github.com/user-attachments/assets/e413584b-8819-4e04-a077-f18b2178c8ec" />


## Extra Questions - 

### Question-1) What is the difference between cp,mv,and rsync?

### Answer-1) Difference is as follows 
🔹 cp (Copy)
Function: Makes a copy of a file or directory.

The original stays in place, and a duplicate is created.

Basic usage:

cp source.txt destination.txt
Options:

-r → copy directories recursively.

-i → ask before overwrite.

-u → only copy if source is newer.

✅ Good for simple duplication.
❌ Doesn’t preserve permissions/timestamps by default (unless -p).

🔹 mv (Move/Rename)
Function: Moves or renames files/directories.

The file is removed from the source location and placed at the destination.

Usage:

mv oldname.txt newname.txt     # Rename
mv file.txt /home/user/docs/   # Move

✅ Efficient because it usually just updates the filesystem pointer.
❌ If moving across filesystems/disks, it works like cp + rm.

🔹 rsync (Remote Sync)
Function: Advanced tool for synchronizing files/directories between locations (local or remote).

Usage:

rsync -avh source/ backup/

Features:
- Incremental → only copies changed parts, not the whole file.
- Remote support → can sync via SSH to another computer.
- Preserves permissions, timestamps, symbolic links, etc.

Useful for backups and mirroring.

✅ Best for efficient backups & syncing.
❌ More complex than cp or mv.

### Question-2. How can you schedule scripts to run automatically?
### Answer-2. Using at command (one-time scheduling)

- If you just want to run a script later (not repeatedly):

1. Install at if not present:

```bash
sudo apt install at
```

2. Enable the service:

```bash
sudo systemctl enable --now atd
```

3. Schedule your script:

```bash
echo "/home/tanya/myscript.sh" | at 5pm
```

(This will run it today at 5 PM).
