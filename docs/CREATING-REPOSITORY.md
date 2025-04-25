# Creating a PockOS JSON Repository

This guide provides detailed instructions on how to create and maintain a JSON repository for PockOS packages. It complements the main README.md with more specific examples and step-by-step instructions.

## What is a PockOS Repository?

A PockOS repository is a JSON-based catalog that contains metadata about applications, libraries, and core components available for the PockOS operating system. The repository is defined in a single `index.json` file that follows a specific structure.

## Step-by-Step Guide

### 1. Create the Basic Structure

Start by creating an `index.json` file with this basic structure:

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

### 2. Define Store Information

The `store` object contains information about your package store:

- `name`: A user-friendly name for your store (e.g., "Pockages")
- `fallback`: A URL that PockOS can use if the local repository is unavailable

### 3. Add Repository Metadata

Fill in the repository metadata:

- `name`: The official name of your repository
- `version`: The version of your repository format (typically "1.0.0")
- `description`: A brief description of what your repository contains

### 4. Add Maintainers

Add information about the repository maintainers:

```json
"maintainers": [
  {
    "name": "Your Full Name",
    "handle": "your-username",
    "github": "https://github.com/your-username"
  },
  {
    "name": "Another Maintainer",
    "handle": "another-username",
    "github": "https://github.com/another-username"
  }
]
```

### 5. Add Packages

The most important part of your repository is the `packages` array. Each package requires specific fields:

#### Required Fields for All Packages

- `id`: A unique identifier for the package (e.g., "gallery")
- `name`: The display name of the package (e.g., "Photos")
- `type`: The type of package ("core", "app", "libro", or "package")
- `package`: The package namespace in reverse domain notation (e.g., "com.pockos.gallery")
- `version`: The version of the package using semantic versioning
- `icon`: The filename of the package icon
- `download`: The URL where the package can be downloaded

#### Optional Fields

- `description`: A brief description of the package

## Package Type Examples

### Core System Component

```json
{
  "id": "java-runtime",
  "name": "Java Runtime Environment",
  "type": "core",
  "package": "com.pockvm.runtime",
  "version": "1.0.0",
  "icon": "Java.png",
  "download": "https://pockos.org/store/downloads/java-runtime.app"
}
```

### Application

```json
{
  "id": "gallery",
  "name": "Photos",
  "type": "app",
  "package": "com.pockos.gallery",
  "version": "2.1.0",
  "icon": "gallery.png",
  "description": "Simple and fast photo viewer optimized for joystick controls",
  "download": "https://pockos.org/store/downloads/gallery.app"
}
```

### Library/Framework

```json
{
  "id": "pockat-framework",
  "name": "Pockat",
  "type": "libro",
  "package": "com.pockos.pockat",
  "version": "1.0.0",
  "icon": "Pockat.png",
  "description": "React-style UI framework for building PockOS apps",
  "download": "https://pockos.org/store/downloads/pockat-framework.app"
}
```

### Other Package

```json
{
  "id": "x86-sim",
  "name": "x86 Simulator",
  "type": "package",
  "package": "com.pockos.sim.x86",
  "version": "0.9.3",
  "icon": "x86.png",
  "download": "https://pockos.org/store/downloads/x86-sim.app"
}
```

## Complete Example

Here's a complete example of an `index.json` file for a small repository:

```json
{
  "store": {
    "name": "My PockOS Store",
    "fallback": "https://my-pockos-store.com"
  },
  "name": "My PockOS Repository",
  "version": "1.0.0",
  "description": "A collection of games and utilities for PockOS",
  "maintainers": [
    {
      "name": "Jane Doe",
      "handle": "janedoe",
      "github": "https://github.com/janedoe"
    }
  ],
  "packages": [
    {
      "id": "calculator",
      "name": "Calculator",
      "type": "app",
      "package": "com.example.calculator",
      "version": "1.0.0",
      "icon": "calculator.png",
      "description": "A simple calculator app",
      "download": "https://my-pockos-store.com/downloads/calculator.app"
    },
    {
      "id": "tetris",
      "name": "Tetris",
      "type": "app",
      "package": "com.example.games.tetris",
      "version": "1.2.0",
      "icon": "tetris.png",
      "description": "Classic Tetris game",
      "download": "https://my-pockos-store.com/downloads/tetris.app"
    }
  ]
}
```

## Validation and Testing

Before publishing your repository, validate your JSON file:

1. Use a JSON validator to check for syntax errors
2. Ensure all required fields are present for each package
3. Verify that all download URLs are accessible
4. Check that all package IDs are unique

## Updating Your Repository

When updating your repository:

1. Increment the version number of packages that have been updated
2. Add new packages to the end of the `packages` array
3. Consider incrementing the repository version if making significant changes

## Publishing Your Repository

To make your repository available to PockOS users:

1. Host your `index.json` file on a web server
2. Ensure the file is served with the correct MIME type (`application/json`)
3. Share the URL of your repository with users

Users can then add your repository to their PockOS system by entering the URL in the package manager settings.

## Tips for Repository Maintenance

- Keep your package descriptions concise but informative
- Use consistent naming conventions for package IDs
- Regularly check that all download links are working
- Update package versions when releasing new versions
- Consider using a CDN for hosting package downloads to improve reliability

## Common Issues and Solutions

### JSON Syntax Errors

If your repository isn't loading, check for JSON syntax errors such as:
- Missing commas between objects
- Extra commas after the last item in an array
- Unclosed brackets or braces
- Unquoted property names

### Package Not Appearing

If a package isn't appearing in the PockOS store:
- Verify that all required fields are present
- Check that the package ID is unique
- Ensure the package type is one of the supported types

### Download Issues

If packages can't be downloaded:
- Verify that the download URL is correct and accessible
- Check that the server is properly configured to serve the file type
- Ensure the file at the download URL is a valid PockOS package