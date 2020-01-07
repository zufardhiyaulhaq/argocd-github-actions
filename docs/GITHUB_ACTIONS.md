# GitHub Actions CI
You can build your apps from repository directly into Docker Hub via GitHub Actions. See [Build, Tag, Publish Docker](https://github.com/marketplace/actions/build-tag-publish-docker) article.

Example:
```
name: Docker Image CI
on:
  create:
    tags:
      - v*
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v1
    - name: Set env
      run: echo ::set-env name=RELEASE_VERSION::$(echo ${GITHUB_REF:10})
    - uses: azure/docker-login@v1
      with:
        login-server: 'index.docker.io'
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}
    - name: Build the Docker image
      run: docker build ./src --file Dockerfile -t zufardhiyaulhaq/gosimplehttp:$RELEASE_VERSION
    - name: Publish the Docker image
      run: docker push zufardhiyaulhaq/gosimplehttp:$RELEASE_VERSION
```
