# Json-Schema-Action-Compression

Uses the [JsonSchemaValidationCompressor.Net](https://github.com/DaanV2/JsonSchemaValidationCompressor.Net) program to condense json validation schemas. this Must be run on windows

## Compression File format

```json
{
  "$schema": "https://raw.githubusercontent.com/DaanV2/JsonSchemaValidationCompressor.Net/master/Schema/Compression%20Schema.json",
  "Files": [
    {
      "Source": "./skinpacks/skins.json",
      "Destination": "../skinpacks/skins.json"
    }
  ]
}
```

## Inputs

**specificationFile**:
The filepath to the specification file.

## Example usage

```yml
# This is a basic workflow to help you get started with Actions

name: Compressing json schemas

# Controls when the action will run. 
on:
  # Triggers the workflow on push or pull request events but only for the master branch
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

  # Allows you to run this workflow manually from the Actions tab
  workflow_dispatch:

# A workflow run is made up of one or more jobs that can run sequentially or in parallel
jobs:
  # This workflow contains a single job called "build"
  build:
    # The type of runner that the job will run on
    runs-on: linux-latest

    # Steps represent a sequence of tasks that will be executed as part of the job
    steps:
      - uses: actions/checkout@v2.3.4

      # Runs a single command using the runners shell
      - uses: DaanV2/Json-Schema-Action-Compression@v2.0
        with:
          specificationFile: "${{github.workspace}}\\source\\compress_specification.json"

      - name: Commit changes
        continue-on-error: true
        run: |
          cd ${{github.workspace}}
          git config --global user.email "Bot@Example.com"
          git config --global user.name "Example Bot"
          git add .
          git commit -m "auto: Generated typescript includes"
          git push
```
