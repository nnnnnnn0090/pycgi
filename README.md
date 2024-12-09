# pycgi

**pycgi** is a lightweight web server solution that allows you to embed Python code directly into HTML files, similar to how PHP works. By using `<?py ?>` tags, you can dynamically generate web pages with the power of Python.

## Features

- **Embed Python in HTML**: Use `<?py ?>` tags to embed Python code inside your HTML files.
- **Dynamic Content Generation**: Generate dynamic web pages by mixing static HTML and Python logic.
- **Simple and Intuitive**: Just like PHP, no need for complex configurations. Write HTML and Python together in one file.
- **Request Handling**: Access request headers, query parameters, and POST data easily.
- **Response Manipulation**: Set response headers and body content directly from your Python code.
- **Flexible Output**: Use the `echo` function to render content directly to the output stream at any point in your HTML.
- **Execution Path Access**: Use `_EXECUTE_PATH` to display the execution path of the running **pycgi** instance.
- **Document Root Access**: Use `_DOCSROOT` to get the document root directory where your `.pycgi` files are located.
- **Storage API**: Easily store and retrieve key-value pairs using the `Storage` object.

## Example

Here’s an example of how you can use **pycgi** to handle request data, set response headers, and use the `echo` function, including displaying the execution path and document root:

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
      # Set a response header
      _RSP_HEADERS["Content-Type"] = "text/html; charset=utf-8"
      _RSP_HEADERS["Custom-Header"] = "MyHeaderValue"

      # Display the execution path
      echo(f"<p>Execution Path: {_EXECUTE_PATH}</p>")

      # Display the document root
      echo(f"<p>Document Root: {_DOCSROOT}</p>")

      # Use echo to render content
      echo("<p>This is rendered using echo.</p>")

      # Print request headers
      for header, value in _REQ_HEADERS.items():
          echo(f"<p>{header}: {value}</p>")
      
      # Print GET query parameter
      if "name" in _GET:
          echo(f"<p>Hello, {_GET['name']}!</p>")
      
      # Print POST data
      if _POST_DATA:
          echo("<p>POST Data:</p><pre>")
          echo(_POST_DATA)
          echo("</pre>")
      
      # Print JSON POST data
      if _POST_JSON:
          echo("<p>JSON POST Data:</p><pre>")
          echo(_POST_JSON)
          echo("</pre>")

      # Storage API Example
      # Set a value in the storage
      Storage.setValue("nickname", "pycgi")

      # Retrieve the value from the storage with a default value
      nickname = Storage.getValue("nickname", "none")
      echo(f"<p>Stored Nickname: {nickname}</p>")
    ?>
    
</body>
</html>
```

In the above example:
- **Storage API**: Demonstrates how to store and retrieve values using the `Storage` object with `Storage.setValue(key, value)` and `Storage.getValue(key, default)` methods.
- **Execution Path**: Display the current execution path of the **pycgi** instance using `_EXECUTE_PATH`.
- **Document Root**: Display the document root directory using `_DOCSROOT`.
- **Response Headers**: Set response headers using the `_RSP_HEADERS` dictionary.
- **Dynamic Output**: Use the `echo` function to render HTML content directly to the output stream, allowing you to inject content at any point in your HTML.

## Getting Started

### 1. Download and Run

1. Download the latest version of **pycgi** from the [Release page](https://github.com/nnnnnnn0090/pycgi/releases).

2. Once downloaded, you can run the server by simply double-clicking on `pycgi`.

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
          echo("<p>This is Python inside HTML!</p>")
        ?>
    </body>
    </html>
    ```

2. Open your web browser and visit `http://localhost:8000/index.pycgi` to see your newly created page.

## Storage API

**pycgi** now includes a simple Storage API that allows you to store and retrieve key-value pairs during the execution of your web application.

- **Store a Value**: You can store a value in the storage by calling `Storage.setValue(key, value)`.

  ```python
  Storage.setValue("nickname", "pycgi")
  ```

- **Retrieve a Value**: To retrieve a value from the storage, use `Storage.getValue(key, default)`. If the key is not found, it will return the default value you provide.

  ```python
  nickname = Storage.getValue("nickname", "none")
  echo(f"Stored Nickname: {nickname}")
  ```

This feature is useful for temporarily storing data during the execution of a request, such as user session information or other dynamic content.

## Request Handling

**pycgi** allows you to handle various types of requests seamlessly:

- **Request Headers**: Access headers via the `_REQ_HEADERS` dictionary.
  
  ```python
  echo(_REQ_HEADERS["Header-Name"])
  ```

- **GET Parameters**: Access GET parameters using the `_GET` dictionary.

  ```python
  echo(_GET["parameter_name"])
  ```

- **POST Data**: Access raw POST data through the `_POST_DATA` variable.

  ```python
  echo(_POST_DATA)
  ```

- **JSON POST Data**: If you send JSON data in the POST request, access it via the `_POST_JSON` variable.

  ```python
  echo(_POST_JSON["key_name"])
  ```

## Response Manipulation

You can modify the HTTP response before it is sent back to the client:

- **Set Response Headers**: Add or modify response headers using the `_RSP_HEADERS` dictionary.

  ```python
  _RSP_HEADERS["Header-Name"] = "Header Value"
  ```

- **Set Response Body**: You can define the response body using the `_RSP_BODY` variable. However, using `echo` allows you to output content directly within your HTML structure.

  ```python
  _RSP_BODY = "<h2>This is the response body.</h2>"
  ```
  
## Options
```python
-h, --help   show this help message and exit
--port PORT  Port to run the server on
```

## How it Works

**pycgi** processes files with a `.pycgi` extension, scanning for any Python code blocks between `<?py ?>` tags. It executes the Python code and replaces the tags with the corresponding output in the HTML, rendering the final result to the user’s browser.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Contact

For questions or feedback, feel free to open an issue or contact me at `nnnnnnn0090@gmail.com`.
