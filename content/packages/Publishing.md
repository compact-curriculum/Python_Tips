+++
title = 'Publishing'
date = 2024-04-25T10:26:01-07:00
draft = false
weight = 2
+++

### Create PyPI accounts

Start by creating an account on these two websites:

1. [**PyPI**](https://pypi.org/): Python package index (PyPI) is a repository for Python packages.
2. [**TestPyPI**](https://test.pypi.org/): TestPyPI is the sister site for PyPI which allows for testing deployment of packages before full deployment.

You will need to authenticate with an app or USB key.
You will also need to save recovery keys for your accounts.

### Get API keys for GitHub actions

On PyPI go to "Account Settings" > "Add API token". Pick a name and then copy the API token.

On your GitHub repo, go to "Settings" > "Secrets and variables" > "Actions" > "Repository secrets"

Add a "New repository secret" and name it "PYPI_API_TOKEN". In the "secret" content section, add the token that you copied from PyPI.

### Add setup.py

Copy this file [setup.py](/Python_Tips/files/setup.py) and fill out the information for your app. Place this file in your root project directory

### Add action script

Copy this file [publish.yml](/Python_Tips/files/publish.yml) and add it to this directory with the structure specified below.

    .
    |-- Root_project_directory/
        |-- .github/
            |-- workflows/
                |-- Publish.yml

### Change Github settings

In your Github repo go to "Settings" > "Pages" and change "Build and deployment source" to "Github Actions"

### Execute actions using a commit

To submit a new version of your package to PyPI, increment the version number in the setup.py file. If the version already exists on PyPI, the package will not be published which is useful for small developmental commits before releasing a new version.

### Going beyond publishing packages

Note that most of the `.yml` file is used to set up the correct environment for the GitHub Actions command. The actual commands are at the bottom of the script:

```yaml
run: | # Execute a multi-line script
  python setup.py sdist bdist_wheel # Run setup.py to create a source distribution and wheel
  twine upload dist/* # Use twine to upload the distribution packages in the dist/ directory to PyPI
```

You can modify this template with any command you want to execute including:

- Publishing a website
- Reviewing code
- Running tests
- Email notifications
- etc...

In practice, it is best to just look up the correct `.yml` file for specific actions as there are many easily accessible resources.
