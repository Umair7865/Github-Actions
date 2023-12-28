Create a .github/workflows directory in your repository on GitHub if this directory does not already exist.

In the .github/workflows directory, create a file named github-actions-demo.yml. For more information, see "Creating new files."

Copy the following YAML contents into the github-actions-demo.yml file:

YAML

name: My First GitHub Actions

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    strategy:
      matrix:
        python-version: [3.8, 3.9]

    steps:
    - uses: actions/checkout@v3
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install pytest
    - name: Run tests
      run: |
        cd src
        python -m pytest addition.py
