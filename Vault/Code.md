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

# Creating notes with random links across folders
for folder_name in folder_names:
    folder_path = os.path.join(vault_path, folder_name)
    for i in range(25):
        file_name = f"{folder_name}_{i+1}.md"
        file_path = os.path.join(folder_path, file_name)
        with open(file_path, 'w') as f:
            f.write(f"#{folder_name} \n [[{folder_name}]]")  # Write the header and self-link

            # Generate random links across folders
            num_links = random.randint(1, 3)  # Generate 1 to 3 links
            for _ in range(num_links):
                linked_folder = random.choice(folder_names)
                if linked_folder != folder_name:  # Ensure it's not the same folder
                    linked_note = f"{linked_folder}_{random.randint(1, 25)}.md"  # Choose a random note within the linked folder
                    f.write(f"\n[[{linked_folder}/{linked_note}]]") 

```