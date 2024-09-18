# Not Hot Dog

![alt text](image.png)

## Detect "Not Hot Dogs" with hugging face API.

**Prerequisites:** *[Hugging Face](https://huggingface.co/), HTML, Python Fundamentals*

**Project Description:** This project uses the Hugging Face API to detect whether an image contains a hot dog or not. The API uses a pre-trained model to classify the image as either a hot dog or not a hot dog. The project also includes a simple HTML interface to upload an image and display the results.

**Let's get started! 🌭**

### Setting Up

1. Create a new directory named nothotdog. This is where our project will live.

   for example:

    ```bash
    mkdir nothotdog
    ```

2. Change into the nothotdog directory.

    ```bash
    cd nothotdog
    ```

3. Create a new Python virtual environment.

    > *Let's create a virtual environment or venv, which is an isolated environment that contains a Python installation in addition to other packages. If you want to learn more check out this [link](https://docs.python.org/3/tutorial/venv.html).*

    ```bash
    python3 -m venv .venv
    ```

4. Activate the virtual environment.

    ```bash
    source venv/bin/activate
    ```

5. Install Flask

   > *Now we are going to install Flask, which is a web framework in Python that makes it easy create to web applications and APIs. You can read more about it [here](https://flask.palletsprojects.com/en/2.2.x/).*

    ```bash
    python -m pip install flask
    ```

6.  Install Dotenv
    
    > *Dotenv is a Python module that reads key-value pairs from a .env file and can set them as environment variables. You can read more about it [here](https://pypi.org/project/python-dotenv/).*

    ```bash
    python -m pip install python-dotenv
    ```

7. Install Requests

    > *Requests is a Python module that allows you to send HTTP requests using Python. You can read more about it [here](https://pypi.org/project/requests/).*

    ```bash
    python -m pip install requests
    ```

8. Create a templates folder for our HTML

    ```bash
    mkdir templates
    ```
  
   > *In Flask, if we are going to have HTML files we typically store them in a folder called templates so Flask is able to find them. Create a folder called templates, which should end up looking like this:*

    ```bash
    nothotdog
    ├── templates
    └── venv
    ```

9. Create a file called `index.html`

    ```bash
    touch templates/index.html
    ```

10. Add the HTML code

    ```html
    <!DOCTYPE html>
    <html lang="en">
      <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <title>Hot dog or Not Hot dog?</title>

        <style>
          body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
          }

          h1 {
            margin-top: 50px;
            color: #333;
            font-size: 2.5rem;
          }

          form {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            width: 100%;
            max-width: 400px;
            margin: 20px auto;
          }

          input[type="file"] {
            margin-bottom: 20px;
            padding: 10px;
            border-radius: 4px;
            border: 1px solid #ccc;
            width: 100%;
          }

          input[type="submit"] {
            background-color: #4caf50;
            color: white;
            padding: 14px 20px;
            margin: 8px 0;
            border: none;
            cursor: pointer;
            border-radius: 4px;
            width: 100%;
            font-size: 1rem;
          }

          input[type="submit"]:hover {
            background-color: #45a049;
          }
        </style>
      </head>
      <body>
        <h1>Hot dog or Not Hot dog?</h1>

        <form method="post" action="{{ url_for('upload') }}" enctype="multipart/form-data">
          <label for="file1">Upload an image:</label>
          <input type="file" name="file1" id="file1" accept="image/*" required />
          <input type="submit" value="Submit" />
        </form>
      </body>
    </html>
    ```

11. Create a file called `web.py`

    ```bash
    touch web.py
    ```

12. Add the Python code

    ```python
    from flask import Flask, render_template, request, jsonify
    import requests
    import json
    import os
    from dotenv import load_dotenv

    load_dotenv()

    API_URL = os.getenv("HUGGING_FACE_API_URL")
    headers = {'Authorization': f'Bearer {os.getenv("HUGGING_FACE_API_KEY")}'}

    app = Flask(__name__)

    def query(data):
        response = requests.request('POST', API_URL, headers=headers, data=data)
        return json.loads(response.content.decode('utf-8'))

    @app.route('/')
    def index():
        return render_template('./index.html')

    @app.route('/upload', methods=['POST'])
    def upload():
        file = request.files['file1']
        modeldata = query(file)
        return jsonify(modeldata)

    app.run(host='0.0.0.0', port=81)
    ```

13. Create a `.env` file

    ```bash
    touch .env
    ```

14. Add the API URL and API Key to the `.env` file

    ```bash
    HUGGING_FACE_API_URL=https://api-inference.huggingface.co/models/simon-mooney/not-hot-dog
    HUGGING_FACE_API_KEY=
    ```

    > ***Note:** HUGGING_FACE_API_KEY=, ading in your API key and URL. This is where we place the hugging face data to allow us to use hugging face's models.*
    > 
    > *You can get your API key by signing up for a free account at [Hugging Face](https://huggingface.co/). and create a token https://huggingface.co/settings/tokens.*


15. Now run the project.

    ```bash
    python web.py
    ```

16. Open your browser

    ```bash
     * Running on all addresses (0.0.0.0)
     * Running on http://127.0.0.1:81
     * Running on http://192.168.71.231:81
    ```

    > *Open your browser and go to http://127.0.0.1:81 or http://192.168.71.231:81.

17. Upload an image

    > *You can now upload an image and see if it is a hot dog or not a hot dog.*
    > *You should see the results displayed on the screen.*

### Conclusion

Congratulations! You have successfully created a project that uses the Hugging Face API to detect whether an image contains a hot dog or not. You have also created a simple HTML interface to upload an image and display the results. You can now use this project to classify images as hot dogs or not hot dogs. 🌭 