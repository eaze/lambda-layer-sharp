# AWS Sharp layer
This AWS lambda layer contains a pre-built [sharp](https://www.npmjs.com/package/sharp) npm library.
It is optimized to reduce the total payload size.

|Sharp version|Layer size (zipped)|Lambda space usage|
|---|---|---|
|[0.26.0](https://github.com/lovell/sharp/releases/tag/v0.26.0)|33.3MB (10.2MB)|

# Getting
A pre-built layer zip file is available at [`dist/sharp-layer.zip`](./dist/sharp-layer.zip).

# Building

## Dependencies
* Docker

1. Clone the repo:
    ```shell script
    git clone git@github.com:Umkus/lambda-layer-sharp.git
    cd lambda-layer-sharp/
    ```

1. Run Docker if it's not already.

1. Build
    ```shell script
    npm run build
    ```
    This will install and then build within a `lambci/lambda` docker image.
    Then the compiled binaries will be copied to `dist` and zip archived.
    Finally it will execute a `require`. If the result output is function methods, then the build succeeded.

1. Import created layer into your AWS account:
    ```shell script
    aws lambda publish-layer-version \
       --layer-name sharp \
       --description "Sharp layer for image resizer" \
       --license-info "Apache License 2.0" \
       --zip-file fileb://dist/sharp-layer.zip \
       --compatible-runtimes nodejs12.x
    ```
