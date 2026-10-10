
Here's an example of a Python function that reads the content of a file:

```python
def read_file(filename):
    """
    Reads the content of a specified file.

    Args:
        filename (str): The path to the file to be read.

    Returns:
        str: The content of the file or an error message if not found.
    """
    try:
        with open(filename, 'r') as file:
            return file.read()
    except FileNotFoundError:
        return f"Error: The file {filename} was not found."

# Example usage
if __name__ == "__main__":
    content = read_file("example.txt")
    print(content)
```

In this code:
- `open(filename, 'r')` opens the file in read mode.
- The `with` statement ensures the file is properly closed after reading, even if an error occurs.
- `file.read()` reads the entire content of the file into a string.
- The `try-except` block handles cases where the file might not exist.
