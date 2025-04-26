# PockOS Package Repository Documentation

This repository serves as a package store for PockOS, containing various applications, libraries, and core components. While the repository metadata is public for transparency, all packages are protected using our proprietary archive format and robust signing system (see [SECURITY.md](SECURITY.md) for details). This documentation explains the structure of the repository and how to create or contribute to a PockOS JSON repository.

## Repository Structure

The PockOS package repository is defined by a single `index.json` file that contains all the metadata about the store and its packages. This file follows a specific structure that allows the PockOS system to discover and install applications and libraries.

### Root Structure

The root of the `index.json` file contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `store` | Object | Contains store-specific information |
| `name` | String | The name of the repository |
| `version` | String | The version of the repository format |
| `description` | String | A brief description of the repository |
| `maintainers` | Array | List of repository maintainers |
| `packages` | Array | List of all packages in the repository |

### Store Object

The `store` object contains the following fields:

| Field | Type | Description |
|-------|------|-------------|
| `name` | String | The display name of the store |
| `fallback` | String | The URL to use if the local repository is unavailable |

### Maintainers Array

Each maintainer object in the `maintainers` array contains:

| Field | Type | Description |
|-------|------|-------------|
| `name` | String | The full name of the maintainer |
| `handle` | String | The username or handle of the maintainer |
| `github` | String | The GitHub profile URL of the maintainer |

### Packages Array

Each package object in the `packages` array contains:

| Field | Type | Description |
|-------|------|-------------|
| `id` | String | Unique identifier for the package |
| `name` | String | Display name of the package |
| `type` | String | Type of package (see Package Types section) |
| `package` | String | The package namespace (typically in reverse domain notation) |
| `version` | String | The version of the package |
| `icon` | String | Filename of the package icon |
| `description` | String (optional) | A brief description of the package |
| `screenshots` | Array (optional) | List of screenshot image filenames (2-6 images) |
| `download` | String | URL to download the package |
| `github_username` | String | The GitHub username of the package developer |

## Package Types

The PockOS repository supports several types of packages:

| Type | Description |
|------|-------------|
| `core` | Essential system components (e.g., Java Runtime, System Settings) |
| `app` | User applications (e.g., Photos) |
| `libro` | Libraries and frameworks for developers (e.g., Pockat) |
| `package` | Other installable packages (e.g., x86 Simulator) |
| `content` | Content packages for specific applications (e.g., GBA games) |

### Content Package Type

Content packages are a special type that provide additional content for specific applications. Important characteristics:

- Content packages must specify a `package` name that matches the target application's package name
- Only applications with the matching package name can access and download the content
- This ensures content is only accessible to its intended application
- Applications can query the repository for content packages that match their package name
- This allows for expandable application content while maintaining security

## How to Create a JSON Repository

### Step 1: Create the Basic Structure

Start by creating an `index.json` file with the basic repository information:

```json
{
  "store": {
    "name": "Your Store Name",
    "fallback": "https://your-domain.com/store"
  },
  "name": "Your Repository Name",
  "version": "1.0.0",
  "description": "Description of your repository",
  "maintainers": [],
  "packages": []
}
```

### Step 2: Add Maintainers

Add information about the repository maintainers:

```json
"maintainers": [
  {
    "name": "Your Name",
    "handle": "your-username",
    "github": "https://github.com/your-username"
  }
]
```

### Step 3: Add Packages

Add packages to your repository:

```json
"packages": [
  {
    "id": "your-app-id",
    "name": "Your App Name",
    "type": "app",
    "package": "com.yourdomain.yourapp",
    "version": "1.0.0",
    "icon": "your-app-icon.png",
    "description": "Description of your app",
    "download": "https://your-domain.com/store/downloads/your-app.app"
  }
]
```

## Example: Adding a New Package

Here's an example of adding a new game application to the repository:

```json
{
  "id": "snake-game",
  "name": "Snake Game",
  "type": "app",
  "package": "com.pockos.games.snake",
  "version": "1.0.0",
  "icon": "snake.png",
  "description": "Classic Snake game optimized for PockOS",
  "screenshots": [
    "snake-screenshot1.png",
    "snake-screenshot2.png",
    "snake-screenshot3.png"
  ],
  "download": "https://pockos.org/store/downloads/snake-game.app"
}
```

### Example: Adding Content for an App

Here's an example of adding content for the GBA emulator:

```json
{
  "id": "pokemon-emerald",
  "name": "Pokemon Emerald",
  "type": "content",
  "package": "com.pockos.gba",
  "version": "1.0.0",
  "icon": "pokemon-emerald.png",
  "description": "Pokemon Emerald game for GBA Emulator",
  "screenshots": [
    "pokemon-em-screenshot1.png",
    "pokemon-em-screenshot2.png",
    "pokemon-em-screenshot3.png",
    "pokemon-em-screenshot4.png"
  ],
  "download": "https://pockos.org/store/downloads/pokemon-emerald.rom"
}
```

## Best Practices

1. **Unique IDs**: Ensure each package has a unique `id` value
2. **Versioning**: Use semantic versioning (MAJOR.MINOR.PATCH) for package versions
3. **Package Naming**: Use reverse domain notation for package namespaces
4. **Icons**: Provide clear, recognizable icons for all packages
5. **Descriptions**: Write concise but informative descriptions
6. **Download URLs**: Ensure download URLs are stable and accessible

## Validating Your Repository

Before publishing your repository, validate your JSON file to ensure it's properly formatted and contains all required fields. You can use online JSON validators or tools like `jsonlint` to check your file.

## Hosting Your Repository

You can host your repository on any web server that can serve static JSON files. Common options include:

- GitHub Pages
- Netlify
- Vercel
- Your own web server

Make sure to set the appropriate MIME type for JSON files (`application/json`) on your server.

## Contributing to the Official Repository

To contribute to the official PockOS repository:

1. Fork the repository
2. Add your package to the `packages` array in `index.json`
3. Ensure your package is properly signed with your developer certificate
4. Verify that all your apps use the same signing keys (if submitting multiple apps)
5. Add developer information to each package:
   - Full name
   - GitHub username
   - Contact information (optional)
6. Submit a pull request following these requirements:
   - Pull request title must include your GitHub username
   - Pull request title must list the packages being added
   - GitHub username must match the developer information in the packages

Maintainers will review your submission and merge it if it meets the quality standards. Note that packages with inconsistent signing keys or unsigned packages will be rejected during the review process.

### Important Notes

- **Consistent Signing Keys**: All packages submitted to the main store index MUST use the same signing key. This is a strict requirement for maintaining security and trust.
- **Alternative Hosting**: If you need to use different signing keys, you can host your packages in a community repository. See the "Hosting Options" section for details.
- **Developer Verification**: Your GitHub username in the pull request must match the developer information in your packages to verify ownership.

## License

This repository is licensed under the MIT License, which means:

- You are free to use, modify, and distribute the repository and its contents
- You can use it for commercial purposes
- The software comes with no warranty or guarantees
- The authors are not liable for any issues arising from its use

See the [LICENSE](LICENSE) file for the complete terms.