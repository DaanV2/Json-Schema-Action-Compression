# Json-Schema-Action-Compression

Uses the [JsonSchemaValidationCompressor.Net](https://github.com/DaanV2/JsonSchemaValidationCompressor.Net) program to condense json validation schemas

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