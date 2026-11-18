# Algorithm for File Updates in Python

**Course:** Google Cybersecurity Professional Certificate — Course 7: Automate Cybersecurity Tasks with Python

## What This Activity Asked For

I was placed in the role of a security professional at a healthcare organization. Access to a restricted subnetwork containing sensitive patient records is controlled by an allow list of approved IP addresses, stored in a text file named `allow_list.txt`. A second list, `remove_list`, identifies IP addresses that should no longer have access. The task was to write a Python algorithm that automatically removes every IP address on `remove_list` from `allow_list.txt`, so the file can be kept up to date without editing it by hand.

## Algorithm Overview

| Step | What the Code Does | Key Concept |
|---|---|---|
| 1 | Open `allow_list.txt` for reading | `with open(..., "r") as file` |
| 2 | Read the contents into a string | `.read()` |
| 3 | Convert the string into a list of IP addresses | `.split()` |
| 4 | Loop through each IP address in `remove_list` | `for` loop |
| 5 | If it is on the allow list, remove it | `if ... in` + `.remove()` |
| 6 | Convert the revised list back into a string | `.join()` |
| 7 | Overwrite the file with the updated contents | `with open(..., "w")` + `.write()` |

## Complete Code

```python
# Assign `import_file` to the name of the file
import_file = "allow_list.txt"

# Build 'with' statement to read in the initial contents of the file
with open(import_file, "r") as file:

    # Use `.read()` to read the imported file and store it in a variable named `ip_addresses`
    ip_addresses = file.read()

# Use `.split()` to convert `ip_addresses` from a string to a list
ip_addresses = ip_addresses.split()

# Build iterative statement
# Name loop variable `element`
# Loop through `remove_list`
for element in remove_list:

    # Build conditional statement
    # If current element is in `ip_addresses`,
    if element in ip_addresses:

        # then current element should be removed from `ip_addresses`
        ip_addresses.remove(element)

# Convert `ip_addresses` back to a string so that it can be written into the text file
ip_addresses = "\n".join(ip_addresses)

# Build `with` statement to rewrite the original file
with open(import_file, "w") as file:

    # Rewrite the file, replacing its contents with `ip_addresses`
    file.write(ip_addresses)
```

`remove_list` is defined earlier in the activity as a list of IP address strings, so it isn't repeated here.

## Step-by-Step Explanation

### 1. Open the allow list file

First, the file name is stored as a string in the `import_file` variable. Then a `with` statement opens it in **read mode**:

```python
import_file = "allow_list.txt"

with open(import_file, "r") as file:
```

- `with` manages the file safely and closes it automatically when the indented block ends.
- `open()` takes two parameters: the file to open, and the mode — `"r"` means read.
- `as file` assigns the variable `file`, which refers to the opened file while inside the `with` block.

### 2. Read the file contents

Inside the `with` block, `.read()` converts the file's contents into one string, stored in `ip_addresses`:

```python
    ip_addresses = file.read()
```

Once the file is a string, it can be processed with ordinary Python operations.

### 3. Convert the string into a list

To remove individual IP addresses, the data has to be a list rather than one long string. `.split()` with no argument splits on whitespace, and since the IP addresses in the file are separated by whitespace, each one becomes its own list element:

```python
ip_addresses = ip_addresses.split()
```

The result is stored back in `ip_addresses`.

### 4. Iterate through the remove list

A `for` loop goes through each IP address in `remove_list`, one at a time, with `element` as the loop variable:

```python
for element in remove_list:
```

The loop runs over `remove_list` (the addresses to delete), and each `element` is then checked against the allow list.

### 5. Remove matching IP addresses

Inside the loop, a conditional checks whether the current `element` is in `ip_addresses` before removing it:

```python
    if element in ip_addresses:
        ip_addresses.remove(element)
```

The check matters because `.remove()` raises an error (`ValueError`) if the value isn't in the list. Guarding it with `if` means an address on `remove_list` that is already absent from the allow list doesn't crash the script. `.remove()` only deletes the **first** occurrence of a value, which works here because the allow list contains no duplicate addresses.

### 6. Convert the list back into a string

`.write()` only accepts string data, so the list is converted back with `.join()`. Using `"\n"` as the separator puts each IP address on its own line, matching the original file format:

```python
ip_addresses = "\n".join(ip_addresses)
```

### 7. Update the file

A second `with` statement opens the same file in **write mode** (`"w"`), which replaces its existing contents with the new string:

```python
with open(import_file, "w") as file:
    file.write(ip_addresses)
```

After this step, `allow_list.txt` no longer contains the removed addresses, so those IP addresses lose access to the restricted content.

## Summary

The algorithm reads `allow_list.txt` into a string, splits it into a list, loops through `remove_list`, and removes each address that is present on the allow list. It then joins the list back into a newline-separated string and overwrites the file with the result. This turns a manual, error-prone update into a repeatable process that can be rerun whenever the remove list changes.

## Reflections / Notes

I checked the code by running it against a small sample `allow_list.txt` and `remove_list`: the addresses on the remove list were deleted, the rest were kept, and the file format stayed one address per line.

---
📄 [View original document](Portfolio%20Activity%207.pdf)

*Part of [security-projects](../).*
