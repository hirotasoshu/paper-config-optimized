
# Minecraft Server Optimized Configurations with Patch Support

This repository provides optimized configurations for Spigot and Paper Minecraft servers, focusing on reducing lag and improving server performance. Additionally, it supports applying JSON patch files to dynamically update server configurations using the `PATCH_DEFINITIONS` environment variable with the `itzg/minecraft-server` Docker image.

## Purpose

This repository is intended to be used with the [Docker Minecraft Server Image](https://github.com/itzg/docker-minecraft-server), offering lag-reducing configurations and the ability to apply patches via JSON files to keep configurations up-to-date and flexible.

## Features

- **Optimized Paper and Spigot configuration files** to minimize lag and maximize performance.
- **Docker compatibility** for easy deployment with the `itzg/docker-minecraft-server` image.
- **Patch support**: Use the `PATCH_DEFINITIONS` environment variable to define a JSON patch file (`patch.json`) that dynamically updates your Minecraft server configurations.
- **Community-driven improvements**: Contributions are welcome! See [Contributing Guidelines](https://github.com/Alpha018/paper-config-optimized/blob/main/CONTRIBUTING.md) to submit your patches and configurations.

## How to Use with Docker and Patches

### Step 1: Clone the Repository

```bash
git clone https://github.com/your-repo/minecraft-server-optimized-config.git
cd minecraft-server-optimized-config
```

### Step 2: Prepare your patch.json file

Create a `patch.json` file that contains the necessary changes to be applied to the default Minecraft server configurations. You can use the structure of patches as shown below:

```json
{
  "patches": [
    {
      "file": "/data/config/paper-world-defaults.yml",
      "ops": [
        {
          "$set": {
            "path": "$._version",
            "value": 30
          }
        }
        // Additional patch operations
      ]
    }
  ]
}
```

### Step 3: Run the Docker Container with the `PATCH_DEFINITIONS` Environment Variable

When starting the Minecraft server with Docker, use the `PATCH_DEFINITIONS` environment variable to point to your `patch.json` file.

```bash
docker run -d -e EULA=TRUE   -e PATCH_DEFINITIONS=/patch.json   -v /path/to/patch.json:/patch.json   -v /path/to/minecraft/config:/data   -p 25565:25565   itzg/minecraft-server
```

In this example:
- `PATCH_DEFINITIONS` is set to `/patch.json`, which refers to the patch file you mounted.
- Configuration files in `/data/config` will be updated based on the operations defined in `patch.json`.

### Step 4: Restart your server for the changes to take effect.

## Contributing

We welcome contributions from the community! If you'd like to add new configurations, patches, or optimize existing ones:
1. Thoroughly test your changes.
2. Open a PR with detailed descriptions of your modifications.
3. Ensure your contributions follow the [Contributing Guidelines](https://github.com/Alpha018/paper-config-optimized/blob/main/CONTRIBUTING.md).

## Version Compatibility

Currently, this repository supports the **latest version** of Minecraft. Contributions for older Minecraft versions are welcome but must be thoroughly tested. Submit a PR with detailed notes.
