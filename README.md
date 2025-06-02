# Json-Schema-Action-Compression

Uses the [JsonSchemaValidationCompressor.Net](https://github.com/DaanV2/JsonSchemaValidationCompressor.Net) program to condense JSON validation schemas. This action runs in a Docker container and works on all GitHub Actions runners.

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
The filepath to the specification file. This should be a relative path from the root of your repository (e.g., `source/compress_specification.json`).

## Example usage

```yml
name: 🖥️ Compress Json Schemas
on:
  push:
    branches:
      - main
    paths:
      - "**/*.json"
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    name: 🖥️ Compress Schemas
    steps:
      - name: 📦 Checkout Repository
        uses: actions/checkout@v4

      - name: 💾 Compress Json
        uses: DaanV2/Json-Schema-Action-Compression@v3.3
        with:
          specificationFile: "source/compress_specification.json"

      - name: ✏️ Commit changes
        continue-on-error: true
        run: |
          cd ${{github.workspace}}
          git config --global user.email "Bot@Example.com"
          git config --global user.name "Example Bot"
          git add .
          git commit -m "auto: generated json schemas"
          git push
```

**Note:**
- The `specificationFile` input should be a relative path (e.g., `source/compress_specification.json`).
- The action runs in Docker, and your repository is mounted at `/github/workspace` inside the container. Relative paths are resolved from the root of your repository.
