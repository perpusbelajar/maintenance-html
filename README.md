# maintenance-html
this repo only for maintenance page using html only
Contoh github workflow
name: Jekyll site CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Build the site in the jekyll/builder container
      run: |
        docker run \
        -v ${{ github.workspace }}:/srv/jekyll -v ${{ github.workspace }}/_site:/srv/jekyll/_site \
        jekyll/builder:latest /bin/bash -c "chmod -R 777 /srv/jekyll && jekyll build --future"
        
  push_image:
    needs: build  # This ensures the 'push_image' job runs only after 'build' has completed
    runs-on: ubuntu-latest

    steps:
    - name: Checkout the repository
      uses: actions/checkout@v4

    - name: Simulate Docker image push (testing)
      run: |
        echo "Simulating Docker image push"
        echo "push success"
        # This simulates a successful push without actually pushing anything
