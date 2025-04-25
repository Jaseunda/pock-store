# PockOS Repository Quick Start Guide

This quick start guide will help you create your own PockOS repository in just a few minutes.

## Prerequisites

- Basic understanding of JSON format
- A text editor
- A web server or hosting service to publish your repository (optional for local testing)

## 5-Minute Setup

### 1. Create Your Repository File

Create a new file named `index.json` with the following structure:

```json
{
  "store": {
    "name": "Your Store Name",
    "fallback": "https://your-domain.com/store"
  },
  "name": "Your Repository Name",
  "version": "1.0.0",
  "description": "Your repository description",
  "maintainers": [
    {
      "name": "Your Name",
      "handle": "your-username",
      "github": "https://github.com/your-username"
    }
  ],
  "packages": []
}
```

### 2. Add Your First Package

Add your first package to the `packages` array:

```json
"packages": [
  {
    "id": "my-first-app",
    "name": "My First App",
    "type": "app",
    "package": "com.yourdomain.firstapp",
    "version": "1.0.0",
    "icon": "app-icon.png",
    "description": "My first PockOS application",
    "download": "https://your-domain.com/downloads/my-first-app.app"
  }
]
```

### 3. Validate Your Repository

Run the validation script to check your repository format:

```bash
node validate-repository.js
```

### 4. Test Locally

You can test your repository locally by pointing your PockOS device to the local file.

### 5. Publish Your Repository

When you're ready, upload your `index.json` file to a web server or hosting service.

## Next Steps

- Add more packages to your repository
- Create icons for your packages
- Set up a proper download server for your packages
- Share your repository URL with other PockOS users

## Resources

- See `README.md` for complete documentation
- See `CREATING-REPOSITORY.md` for detailed instructions
- Use `template.json` as a starting point for your repository
- Run `validate-repository.js` to check your repository for errors

## Common Package Types

- `app`: User applications
- `libro`: Libraries and frameworks
- `core`: System components
- `package`: Other installable packages

## Tips

- Use unique IDs for each package
- Follow semantic versioning (MAJOR.MINOR.PATCH)
- Provide clear, descriptive names and descriptions
- Ensure your download URLs are stable and accessible