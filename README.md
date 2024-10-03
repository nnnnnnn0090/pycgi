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

### 1. Download and Run

1. Download the latest version of **pycgi** from the [Release page](https://github.com/your-repo/pycgi/releases).

2. Once downloaded, extract the files and open a command line (Terminal or Command Prompt). Run the following command to start the server:

    ```bash
    ./pycgi
    ```

   When you run this command, a `docs` folder will automatically be created in the same directory. You can place your `.pycgi` files inside this folder.

### 2. Creating Your First `.pycgi` File

1. Inside the `docs` folder, create a new file named `index.pycgi` with the following content:

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

2. Open your web browser and visit `http://localhost:8000/index.pycgi` to see your newly created page.

## How it Works

**pycgi** processes files with a `.pycgi` extension, scanning for any Python code blocks between `<?py ?>` tags. It executes the Python code and replaces the tags with the corresponding output in the HTML, rendering the final result to the user’s browser.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or feedback, feel free to open an issue or contact me at `nnnnnnn0090@gmail.com`.
