# QuantNexus Plugin Registry

Official plugin registry for [QuantNexus Desktop](https://github.com/SilverstreamsAI/QuantNexus) - a GitHub-based marketplace for discovering, installing, and managing community plugins.

## Repository Structure

```
QuantNexus-plugin-registry/
├── registry.json           # Lightweight plugin index (for fast listing)
├── plugins/                # Detailed metadata per plugin
│   ├── com.example.plugin-a.json
│   └── com.example.plugin-b.json
├── stats/
│   └── stats.json          # Auto-generated stats (downloads, stars)
├── categories.json         # Category definitions
└── .github/workflows/      # Automation scripts
    ├── update_stats.yml    # Daily job to fetch GitHub stars/downloads
    └── validate_pr.yml     # Security checks for submissions
```

## For Plugin Users

The QuantNexus Desktop application automatically fetches plugins from this registry. Simply open the **Plugin Marketplace** in the app to browse, install, and update plugins.

## For Plugin Developers

### Submitting a Plugin

1. **Fork** this repository
2. **Create** a new file `plugins/your.plugin.id.json` following the schema below
3. **Add** your plugin to `registry.json`
4. **Submit** a Pull Request

### Plugin Metadata Schema

```json
{
  "id": "com.yourname.plugin-name",
  "name": "Plugin Display Name",
  "description": "A brief description of what your plugin does",
  "author": {
    "name": "Your Name",
    "github": "your-github-username",
    "email": "your@email.com"
  },
  "repository": "https://github.com/yourname/your-plugin-repo",
  "license": "MIT",
  "categories": ["trading", "indicators"],
  "pricing": {
    "type": "free"
  },
  "permissions": {
    "network": false,
    "filesystem": "plugin",
    "native": false
  },
  "dependencies": {
    "python": ["numpy>=1.20.0"],
    "node": {}
  },
  "versions": [
    {
      "version": "1.0.0",
      "releaseDate": "2026-01-01",
      "downloadUrl": "https://github.com/.../releases/download/v1.0.0/plugin.zip",
      "sha256": "checksum-of-zip-file",
      "minEngine": "0.1.0",
      "changelog": "Initial release"
    }
  ]
}
```

### Permission Levels

| Permission | Values | Description |
|------------|--------|-------------|
| `network` | `true/false` | External API access |
| `filesystem` | `none`, `plugin`, `user` | File system access level |
| `native` | `true/false` | Native module execution (.pyd, .so) |

### Security Requirements

- Download URLs must point to GitHub Releases
- All releases must include SHA256 checksums
- Compiled extensions (.pyd, .so) require manual review

## Automation

- **Daily Stats Update**: GitHub Actions fetches download counts and star ratings
- **PR Validation**: Automated schema validation and security scanning

## License

MIT License - see [LICENSE](LICENSE) for details.
