#code 

```python
import os
import random
from pathlib import Path

# Vault
vault_path = '/Users/aidanastridge/Documents/Base/Vault'

# Eliminating file extensions and cleaning
vault = os.listdir(vault_path)
vault.remove('.DS_Store')  # Mac hidden file

# Creating folders
folder_names = []

for files in vault:
    file_name = Path(files).stem
    folder_names.append(file_name)

for folder_name in folder_names:
    os.makedirs(os.path.join(vault_path, folder_name), exist_ok=True)

# Creating notes with random links
for folder_name in folder_names:
    folder_path = os.path.join(vault_path, folder_name)
    for i in range(25):
        file_name = f"{folder_name}_{i+1}.md"
        file_path = os.path.join(folder_path, file_name)
        with open(file_path, 'w') as f:
            f.write(f"#{folder_name} \n [[{folder_name}]]")

            num_links = random.randint(1, 5)  # Generate 1 to 5 links
            for _ in range(num_links):
                linked_note = random.choice([f"{folder_name}_{j+1}.md" for j in range(25) if j != i])
                f.write(f"\n[[{linked_note}]]")


# Creating "Orphans" folder
orphans_path = os.path.join(vault_path, "Orphans")
os.makedirs(orphans_path, exist_ok=True)

for i in range(75):
    file_name = f"orphan_{i+1}.md"
    file_path = os.path.join(orphans_path, file_name)
    with open(file_path, 'w') as f:
        f.write("")

```