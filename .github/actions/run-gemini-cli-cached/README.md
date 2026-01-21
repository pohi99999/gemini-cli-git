# Run Gemini CLI (Cached)

A reusable composite GitHub Action that runs Gemini CLI with optimized caching for faster execution and reduced costs.

## Features

- ✅ **Smart Caching**: Caches Gemini CLI installation across workflow runs
- ✅ **Fast Execution**: Skips npm install on cache hits (saves ~30-45s per run)
- ✅ **Flexible Configuration**: Support for custom settings and models
- ✅ **Model Selection**: Easy switching between `gemini-3-pro-preview`, `gemini-2.5-flash`, etc.
- ✅ **Error Handling**: Proper error capture and reporting
- ✅ **Artifact Support**: Automatically saves logs to `gemini-artifacts/`

## Usage

```yaml
- name: 'Run Gemini CLI'
  uses: ./.github/actions/run-gemini-cli-cached
  with:
    gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
    gemini_model: 'gemini-3-pro-preview'  # or 'gemini-2.5-flash'
    prompt: |
      Your prompt here...
```

## Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `gemini_api_key` | Conditional | - | Gemini API key for authentication (required unless using Vertex AI) |
| `gemini_model` | No | `gemini-3-pro-preview` | Model to use (e.g., `gemini-2.5-flash` for faster/cheaper) |
| `prompt` | ✅ Yes | - | The prompt to send to Gemini CLI |
| `settings` | No | `{"autoAccept": true, "model": {"temperature": 0.7}}` | JSON settings for Gemini CLI |
| `cache_version` | No | `v1` | Cache version for invalidation (increment to bust cache) |
| **Google Cloud / Vertex AI** | | | |
| `use_vertex_ai` | No | `false` | Use Vertex AI instead of Gemini API |
| `gcp_project_id` | Conditional | - | Google Cloud project ID (required when `use_vertex_ai=true`) |
| `gcp_location` | No | `us-central1` | Google Cloud location |
| `google_api_key` | No | - | Vertex AI API key (alternative to `gemini_api_key`) |
| `gcp_access_token` | No | - | Google Cloud access token (from `google-github-actions/auth` action) |

## Outputs

| Output | Description |
|--------|-------------|
| `stdout` | Standard output from Gemini CLI |
| `stderr` | Standard error from Gemini CLI |
| `success` | Whether Gemini CLI succeeded (`true`/`false`) |

## Examples

### Basic Usage

```yaml
- uses: ./.github/actions/run-gemini-cli-cached
  with:
    gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
    prompt: 'Analyze this code and suggest improvements'
```

### Using Flash Model (Faster & Cheaper)

```yaml
- uses: ./.github/actions/run-gemini-cli-cached
  with:
    gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
    gemini_model: 'gemini-2.5-flash'
    prompt: 'Review this pull request'
```

### Custom Settings

```yaml
- uses: ./.github/actions/run-gemini-cli-cached
  with:
    gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
    gemini_model: 'gemini-3-pro-preview'
    settings: |
      {
        "autoAccept": true,
        "model": {
          "temperature": 0.9,
          "maxTokens": 2048
        }
      }
    prompt: 'Generate creative content'
```

### With Output Handling

```yaml
- name: 'Run Gemini'
  id: gemini
  uses: ./.github/actions/run-gemini-cli-cached
  with:
    gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
    prompt: 'Analyze this'

- name: 'Use Output'
  if: steps.gemini.outputs.success == 'true'
  run: |
    echo "Gemini output: ${{ steps.gemini.outputs.stdout }}"
```

### Using Vertex AI with Workload Identity

```yaml
- name: 'Authenticate to Google Cloud'
  id: auth
  uses: google-github-actions/auth@v2
  with:
    project_id: ${{ vars.GCP_PROJECT_ID }}
    workload_identity_provider: ${{ secrets.WIF_PROVIDER }}
    service_account: ${{ secrets.WIF_SERVICE_ACCOUNT }}
    token_format: 'access_token'

- uses: ./.github/actions/run-gemini-cli-cached
  with:
    use_vertex_ai: 'true'
    gcp_project_id: ${{ vars.GCP_PROJECT_ID }}
    gcp_location: 'us-central1'
    gcp_access_token: ${{ steps.auth.outputs.access_token }}
    gemini_model: 'gemini-3-pro-preview'
    prompt: 'Your prompt here'
```

### Using Vertex AI with API Key

```yaml
- uses: ./.github/actions/run-gemini-cli-cached
  with:
    use_vertex_ai: 'true'
    gcp_project_id: ${{ vars.GCP_PROJECT_ID }}
    google_api_key: ${{ secrets.GOOGLE_API_KEY }}
    gemini_model: 'gemini-3-pro-preview'
    prompt: 'Your prompt here'
```

## Performance

### Benchmark Results

| Scenario | Original | With Caching | Improvement |
|----------|----------|--------------|-------------|
| **First run** (cache miss) | 2m7s | 2m5s | ~2s faster |
| **Subsequent runs** (cache hit) | 2m7s | **36s** | **71% faster** |

### Cache Behavior

- **Cache miss**: Installs Gemini CLI from npm (~30-45s)
- **Cache hit**: Skips installation entirely (~2-3s)
- **Cache key**: `gemini-cli-{OS}-latest-{version}`

## Artifacts

The action automatically creates `gemini-artifacts/` directory with:
- `stdout.log` - Full standard output
- `stderr.log` - Full standard error
- `telemetry.log` - Gemini CLI telemetry (if available)

## Cache Invalidation

To force a fresh installation (bust the cache):

```yaml
- uses: ./.github/actions/run-gemini-cli-cached
  with:
    gemini_api_key: ${{ secrets.GEMINI_API_KEY }}
    cache_version: 'v2'  # Increment this
    prompt: 'Your prompt'
```

## Model Selection Guide

| Model | Speed | Cost | Best For |
|-------|-------|------|----------|
| `gemini-3-pro-preview` | Slower | Higher | Complex reasoning, accuracy-critical tasks |
| `gemini-2.5-flash` | **Faster** | **Lower** | Quick iterations, content generation |

**Recommendation**: Use `gemini-2.5-flash` for most tasks unless you need Pro's advanced reasoning.

## Troubleshooting

### Cache not working?

1. Check cache key is consistent
2. Increment `cache_version` to reset
3. Verify paths are correct for your OS

### Permission errors?

Ensure `GEMINI_API_KEY` is set in repository secrets.

### Installation fails?

Check npm registry is accessible and `@google/gemini-cli` package exists.

## License

Same as parent repository.
