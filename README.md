# SHACL validation action

This action performs SHACL validation based on the [TopQuadrant SHACL API](https://github.com/TopQuadrant/shacl), accepting only `.ttl` format as input.

# Examples
## Classical: file with both data and shapes

You have a `.ttl` file in your repository containing both data and shapes.

```yaml
uses: actions/shacl-validation@v1
with:
  validation-data: 'data.ttl'
```

## Separate shapes file

You have two `.ttl` files in your repository: one with data and one with shapes.

```yaml
uses: actions/shacl-validation@v1
with:
  validation-data: 'data.ttl'
  validation-rules: 'shapes.ttl'
```

# Advanced examples

## Ensuring that a file is invalid

You have a `.ttl` file that must not pass validation and you would like the action to check this without failing.

```yaml
name: invalid-data
uses: actions/shacl-validation@v1
continue-on-error: true
with:
  validation-data: 'invalid_data.ttl'
```

In next steps you should add the following:

```yaml
  - run: echo "Invalid data was indeed invalid"
    if: job.steps.invalid-data.status == failure()
  - run: exit 1
    if: job.steps.invalid-data.status == success()
```

The action will fail if the invalid data passes checks and will succeed if invalid data doesn't pass checks.