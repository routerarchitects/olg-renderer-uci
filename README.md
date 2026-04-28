# OLG Renderer UCI

Collection of ucode templates and helper scripts used to render validated uCentral configuration into UCI batch output.

This repository contains the renderer-side code. Schema validation artifacts are maintained in the companion `olg-ucentral-schema` repository.

## Testing

### Dependencies

To run the test cases you will need:

- [ucode](https://github.com/jow-/ucode)
- `jq`

### Clone Repositories

Clone both repositories into the same parent directory:

```sh
git clone https://github.com/Telecominfraproject/olg-ucentral-schema.git
git clone https://github.com/Telecominfraproject/olg-renderer-uci.git
```
### Copy Schema Reader

The integration tests in `olg-renderer-uci` require `schemareader.uc`, which is generated and maintained in `olg-ucentral-schema`.

```sh
cp olg-ucentral-schema/validator/ucode/schemareader.uc \
   olg-renderer-uci/schemareader.uc
```

The renderer repository root also contains `renderer-schema.json`. Keep this file aligned with the schema version declared in:

- `olg-ucentral-schema/schema.json`

### Validate Test Setup

Before running tests, make sure `olg-ucentral-schema` and `olg-renderer-uci` are checked out to compatible branches or commits.

Verify the version files are aligned:

```sh
cat olg-ucentral-schema/schema.json
cat olg-renderer-uci/renderer-schema.json
```

If needed, switch both repositories to the intended matching branch or commit, then regenerate the schema reader:

```sh
cd olg-ucentral-schema
./tools/generate.sh

cp validator/ucode/schemareader.uc ../olg-renderer-uci/schemareader.uc
```

### Unit Tests

Run only the unit tests:

```sh
cd olg-renderer-uci/tests
./test-runner unit
```

### Integration Tests

Run only the integration tests:

```sh
cd olg-renderer-uci/tests
./test-runner full
```

### Full Test Suite

Run the complete test suite:

```sh
cd olg-renderer-uci/tests
./test-runner
```

### Regenerate Expected Outputs

Regenerate expected outputs for the integration suite:

```sh
cd olg-renderer-uci/tests
./test-runner full copy-to-expected
```

### Installed Files

The following ucode scripts are installed to the target:

- `renderer/*` - renderer sources and templates
- `command/*` - predefined command implementations
- `system/*` - scripts to generate system information such as state, telemetry, health, and capabilities
