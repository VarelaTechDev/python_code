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
