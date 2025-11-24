# Strigo Git Integration - Migration Guide

This repository contains the structure and templates for migrating Strigo console content to GitHub using Strigo's Git integration feature.

## Overview

This migration allows you to:
- Version control your training content
- Use Markdown-based exercises with enhanced features
- Access features not available in the console (duration metadata, info blocks, navigation buttons, lab-challenge validation scripts, richer lab configs)
- Automatically fetch content from GitHub into Strigo

## Repository Structure

```
.
├── .strigo/
│   └── config.yml          # Main configuration file for labs and exercises
├── exercises/
│   ├── introduction.md      # Sample exercise in Markdown format
│   └── hands-on-practice.md # Another sample exercise
├── scripts/
│   ├── user-data.sh        # User data script (runs on EC2 instance launch)
│   ├── setup.sh            # Lab setup script (runs on instance creation)
│   └── teardown.sh         # Lab teardown script (runs on instance destruction)
├── labs/
│   └── default-lab.yml     # Lab configuration file
└── README.md               # This file
```

## Migration Process

### Step 1: Convert Console Content to Markdown

Since Strigo console uses rich-text format and GitHub integration uses Markdown, you need to:

1. **Copy content from Strigo console**
   - Open each exercise in the Strigo management console
   - Copy the text content
   - Copy any images or resources

2. **Create Markdown files**
   - Create a new `.md` file in the `exercises/` directory
   - Convert rich-text formatting to Markdown syntax
   - Add images to a `images/` or `assets/` directory if needed
   - Reference images using Markdown: `![Alt text](images/image.png)`

3. **Enhance with Git-only features**
   - Add duration metadata
   - Use info blocks: `> **Info:** Your info text`
   - Use warning blocks: `> **Warning:** Your warning text`
   - Use note blocks: `> **Note:** Your note text`
   - Add navigation buttons (if applicable)

### Step 2: Configure Lab Settings

1. **Update `.strigo/config.yml`**
   - Define your lab configurations
   - Reference your exercise Markdown files
   - Set lab specifications (CPU, RAM, image, etc.)

2. **Update lab configuration files** (if using separate files)
   - Modify `labs/default-lab.yml` or create new lab configs
   - Set machine size, image, scripts, interfaces

### Step 3: Set Up GitHub Integration in Strigo

1. **Connect Strigo to GitHub**
   - Go to your Strigo account settings
   - Verify your GitHub identity
   - Install the Strigo GitHub app on this repository

2. **Fetch Content in Strigo**
   - Edit your class template in Strigo
   - Click on "Fetch exercises and lab configurations from GitHub"
   - Enter your repository URL: `https://github.com/your-org/your-repo`
   - Specify the branch (usually `main` or `master`)
   - Click "Fetch Exercises" and "Fetch Labs"
   - Save your class template

### Step 4: Remove Old Console Configurations (Optional)

When you're ready to fully migrate:
- The dialog you saw ("Remove lab configurations") allows you to remove old console-based lab configurations
- This is safe to do once you've verified the GitHub integration is working
- Click "OK" to remove old configurations, or "Cancel" to keep them temporarily

## Configuration Files

### `.strigo/config.yml`

This is the main configuration file that Strigo reads. It defines:
- **Labs**: Lab configurations with machine specs, images, scripts, interfaces
- **Exercises**: References to Markdown exercise files

Example structure:
```yaml
labs:
  - name: default-lab
    display_name: Default Lab Configuration
    platform: aws
    machine_size:
      cpu: 2
      ram: 4
    image: ami-003c60acc3656b8db
    user_data: scripts/user-data.sh  # User data script for instance initialization

exercises:
  - name: introduction
    display_name: Introduction Exercise
    file: exercises/introduction.md
    duration: 15
    lab_config: default-lab
```

### Exercise Markdown Files

Exercises are written in Markdown and support:
- Standard Markdown syntax
- Code blocks with syntax highlighting
- Info/Warning/Note blocks
- Duration metadata
- Navigation buttons

## Lab Configuration Options

### Machine Size
- `cpu`: Number of CPU cores
- `ram`: RAM in GB

### Platform Types
- `aws`: Amazon Web Services
- `azure`: Microsoft Azure
- `gcp`: Google Cloud Platform
- `docker`: Docker containers
- `kubernetes`: Kubernetes clusters

### User Data Script
- `user_data`: Path to a bash script that runs when the EC2 instance is launched
- This script typically installs tools, configures the environment, and sets up required services
- The user data script in this repository (`scripts/user-data.sh`) installs:
  - kubectl (Kubernetes CLI)
  - Helm (Kubernetes package manager)
  - AWS CLI v2
  - Terraform
  - krew (kubectl plugin manager)
  - OIDC login plugin for Kubernetes
  - Configures Kubernetes cluster access with Keycloak authentication
  - Sets up Strigo environment variables

### Interfaces
- `ssh`: SSH access
- `rdp`: Remote Desktop Protocol
- `web`: Web interface
- `vnc`: VNC access

## Best Practices

1. **Version Control**
   - Commit changes frequently
   - Use meaningful commit messages
   - Tag releases for stable versions

2. **Content Organization**
   - Keep exercises in the `exercises/` directory
   - Organize by module or topic
   - Use descriptive file names

3. **Testing**
   - Test exercises after migration
   - Verify lab configurations work correctly
   - Check that all resources are accessible

4. **Documentation**
   - Keep README updated
   - Document any custom scripts
   - Note any special requirements

## Resources

- [Strigo Help Article: Fetch Exercises and Lab Configurations from GitHub](https://help.strigo.io/en/articles/4951906-fetch-exercises-and-lab-configurations-from-github)
- [Strigo Example Labs Repository](https://github.com/strigo/strigo-github-labs-examples)

## Next Steps

1. Replace sample exercises with your actual content
2. Update lab configurations to match your requirements
3. Customize setup/teardown scripts as needed
4. Push to GitHub
5. Connect Strigo to fetch from this repository
6. Test the integration
7. Remove old console configurations once verified

## Support

If you encounter issues during migration:
- Review the Strigo help documentation
- Check the example repository for reference
- Contact Strigo support if needed

