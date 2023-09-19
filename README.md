```python
def extract_unique(input_filename, output_filename):
    # Read the file and extract unique right side values
    with open(input_filename, 'r') as file:
        lines = file.readlines()
        right_side_values = set(line.split('=')[1].strip() for line in lines if '=' in line)

    # Write the unique values to a new file
    with open(output_filename, 'w') as file:
        for value in right_side_values:
            file.write(value + '=\n')

    print(f"Unique right-side values saved to {output_filename}")


# Extract unique values from "extract.txt" and write to "links.txt"
extract_unique("extract.txt", "links.txt")
```

```python
def lookup_link(input_filename):
    # Read the link mappings
    with open(input_filename, 'r') as file:
        lines = file.readlines()
        link_mapping = {line.split('=')[0].strip(): line.split('=')[1].strip() for line in lines if '=' in line}

    # Ask user for input and return the corresponding link
    key = input("Enter the right-side value (e.g., _spsGetY): ")
    link = link_mapping.get(key, None)
    if link:
        print(f"Link for {key}: {link}")
    else:
        print(f"No link found for {key}")


# Lookup the link for a value in "links.txt"
lookup_link("links.txt")
```

```python
import os

def extract_javadoc(filename):
    with open(filename, 'r') as file:
        lines = file.readlines()

    # Identify the JavaDoc comment blocks
    inside_javadoc = False
    javadoc_lines = []
    for line in lines:
        if line.strip().startswith('/**') and not line.strip().startswith('/********'):
            inside_javadoc = True
            continue  # skip the line that starts the JavaDoc comment
        if line.strip().endswith('*/') and inside_javadoc:
            inside_javadoc = False
            continue  # skip the line that ends the JavaDoc comment
        if inside_javadoc:
            javadoc_lines.append(line.strip())

    return ' '.join(javadoc_lines)

def search_and_extract(name, directory):
    target_file = os.path.join(directory, name + "Handler.java")
    
    if os.path.exists(target_file):
        javadoc = extract_javadoc(target_file)
        
        # Write to output file
        with open('javadoc_output.txt', 'w') as out_file:
            out_file.write(javadoc)
        
        print(f"JavaDoc extracted to 'javadoc_output.txt'")
    else:
        print(f"File {target_file} not found.")


name = "CHANGE_THE_NAME"
search_and_extract(name, "Files")
```


```python
import os

def extract_javadoc(filename):
    with open(filename, 'r') as file:
        lines = file.readlines()

    # Identify the JavaDoc comment blocks
    inside_javadoc = False
    javadoc_lines = []
    for line in lines:
        if line.strip().startswith('/**') and not line.strip().startswith('/********'):
            inside_javadoc = True
            continue  # skip the line that starts the JavaDoc comment
        if line.strip().endswith('*/') and inside_javadoc:
            inside_javadoc = False
            continue  # skip the line that ends the JavaDoc comment
        if inside_javadoc:
            if "@author" in line:
                break
            javadoc_lines.append(line.strip('*').strip())  # remove leading stars and spaces

    return ' '.join(javadoc_lines).rstrip('*').strip()  # remove trailing stars and spaces

def search_and_extract(name, directory):
    target_file = os.path.join(directory, name + "Handler.java")
    
    if os.path.exists(target_file):
        javadoc = extract_javadoc(target_file)
        
        # Write to output file
        with open('javadoc_output.txt', 'w') as out_file:
            out_file.write(javadoc)
        
        print(f"JavaDoc extracted to 'javadoc_output.txt'")
    else:
        print(f"File {target_file} not found.")

while True:
    name = input("Enter the class name (or type 'exit' to quit): ")
    if name.lower() == "exit":
        break
    search_and_extract(name, "Files")
```
