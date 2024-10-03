# pycgi

**pycgi** is a lightweight web server solution that allows you to embed Python code directly into HTML files, similar to how PHP works. By using `<?py ?>` tags, you can dynamically generate web pages with the power of Python.

## Features

- **Embed Python in HTML**: Use `<?py ?>` tags to embed Python code inside your HTML files.
- **Dynamic Content Generation**: Generate dynamic web pages by mixing static HTML and Python logic.
- **Simple and Intuitive**: Just like PHP, no need for complex configurations. Write HTML and Python together in one file.
  
## Example

Here’s an example of how you can use **pycgi**:

```html
<!DOCTYPE html>
<html>
<head>
    <title>My pycgi Page</title>
</head>
<body>
    <h1>Welcome to pycgi!</h1>
    
    <!-- Static HTML content -->
    <p>This is a static message.</p>
    
    <!-- Embedded Python code -->
    <?py
    for i in range(3):
        print(f"<p>Dynamic message {i+1}</p>")
    ?>
    
</body>
</html>
```

In the above example, the Python code within `<?py ?>` is executed, and its output is rendered directly in the HTML response.

## Getting Started

### Requirements

- Python 3.x

### Creating Your First `.pycgi` File

1. Create a new file in the project directory with the `.pycgi` extension, for example `index.pycgi`:

    ```html
    <!DOCTYPE html>
    <html>
    <head>
        <title>My First pycgi Page</title>
    </head>
    <body>
        <h1>Hello pycgi!</h1>
        
        <?py
        print("<p>This is Python inside HTML!</p>")
        ?>
    </body>
    </html>
    ```

2. Access it by visiting `http://localhost:8000/index.pycgi` in your web browser.

## How it Works

**pycgi** processes files with a `.pycgi` extension, scanning for any Python code blocks between `<?py ?>` tags. It executes the Python code and replaces the tags with the corresponding output in the HTML, rendering the final result to the user’s browser.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or feedback, feel free to open an issue or contact me at `nnnnnnn0090@gmail.com`.
