# Pull Request Guidelines for PockOS Package Repository

## Pull Request Title Format

Your pull request title must follow this format:
```
[GitHub_Username] Add: package1_name, package2_name
```

Example:
```
PockStudio Add: system-utils.app, terminal.pock
```

## Requirements

1. **GitHub Username Verification**
   - Your GitHub username in the PR title must match the developer information in your package metadata
   - This helps verify package ownership and maintain security

2. **Package Listing**
   - List all packages being added in the PR title
   - Separate multiple packages with commas
   - Include the file extension (.app, .pock, or .libro)

3. **Package Formats**
   PockOS supports these proprietary archive formats:
   - `.app`: Standard PockOS applications
   - `.pock`: System extensions and utilities
   - `.libro`: Documentation and content packages

## Verification Process

1. **Repository Verification**
   - Verified repositories are listed in `verified.json`
   - Verified status appears in the PockOS store
   - Users can easily identify trusted packages

2. **Benefits of Verification**
   - Enhanced visibility in the PockOS store
   - User trust and confidence
   - Priority support from the PockOS team

3. **Getting Verified**
   - Submit high-quality packages
   - Maintain consistent signing keys
   - Follow security best practices
   - Regular updates and maintenance

## Additional Resources

- For package creation guidelines, visit [PockOS GitHub](https://github.com/PockStudio)
- Review the verification criteria in `verified.json`
- Check existing verified repositories for best practices

## Questions?

If you have questions about the pull request process or repository verification, please open an issue or contact the PockOS team.