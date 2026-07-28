# Godot MCP (Model Context Protocol)

A comprehensive integration between Godot Engine and AI assistants using the Model Context Protocol (MCP). This plugin allows AI assistants to interact with your Godot projects, providing powerful capabilities for code assistance, scene manipulation, and project management.

## Features

- **Full Godot Project Access**: AI assistants can access and modify scripts, scenes, nodes, and project resources
- **Two-way Communication**: Send project data to AI and apply suggested changes directly in the editor
- **Command Categories**:
  - **Node Commands**: Create, modify, and manage nodes in your scenes
  - **Script Commands**: Edit, analyze, and create GDScript files
  - **Scene Commands**: Manipulate scenes and their structure
  - **Project Commands**: Access project settings and resources
  - **Editor Commands**: Control various editor functionality
  - **Enhanced Commands**: Access full scene tree, debug output, and asset management

## Enhanced Features (New)

This fork adds several significant improvements:

- **Complete Scene Tree Visibility**: Retrieve the entire scene hierarchy with `get_full_scene_tree`
- **Dynamic Script Access**: Read and write any script by path with dynamic resource templates
- **Asset Management**: Query and organize project assets by type (images, audio, models, etc.)
- **Debug Output Access**: Retrieve runtime debug logs from the Godot editor
- **AI Script Generation**: Generate script templates from natural language descriptions
- **Node Transform Tools**: Easily update node position, rotation and scale

## Quick Setup

### 1. Clone the Repository

```bash
git clone https://github.com/waefrebeorn/Godot-MCP.git
cd Godot-MCP
```

### 2. Set Up the MCP Server

```bash
cd server
npm install
npm run build
# Return to project root
cd ..
```

### 3. Set Up Claude Desktop

1. Edit or create the Claude Desktop config file:
   ```bash
   # For macOS
   nano ~/Library/Application\ Support/Claude/claude_desktop_config.json
   # For Windows (PowerShell)
   notepad "$env:APPDATA\Claude\claude_desktop_config.json"
   ```

2. Add the following configuration (or use the included `claude_desktop_config.json` as a reference):
   ```json
   {
     "mcpServers": {
       "godot-mcp": {
         "command": "node",
         "args": [
           "PATH_TO_YOUR_PROJECT/server/dist/index.js"
         ],
         "env": {
           "MCP_TRANSPORT": "stdio"
         }
       }
     }
   }
   ```
   > **Note**: Replace `PATH_TO_YOUR_PROJECT` with the absolute path to where you have this repository stored.

3. Restart Claude Desktop

### 4. Open the Example Project in Godot

1. Open Godot Engine
2. Select "Import" and navigate to the cloned repository
3. Open the `project.godot` file
4. The MCP plugin is already enabled in this example project

## Using MCP with Claude

After setup, you can work with your Godot project directly from Claude using natural language. Here are some examples:

### Example Prompts

```
@mcp godot-mcp read godot://script/current

I need help optimizing my player movement code. Can you suggest improvements?
```

```
@mcp godot-mcp run get-full-scene-tree

Add a cube in the middle of the scene and then make a camera that is looking at the cube.
```

```
@mcp godot-mcp read godot://scene/current

Create an enemy AI that patrols between waypoints and attacks the player when in range.
```

### New Enhanced Commands Examples

```
@mcp godot-mcp read godot://script/res://scripts/player.gd

Please analyze this player script and suggest improvements.
```

```
@mcp godot-mcp run ai_generate_script --description "A health system with damage and healing" --node_type "Node"

Implement this health system in my game.
```

```
@mcp godot-mcp run list_assets_by_type --type images

Show me all the images in my project and help me organize them better.
```

### Natural Language Tasks Claude Can Perform

- "Create a main menu with play, options, and quit buttons"
- "Add collision detection to the player character"
- "Implement a day/night cycle system"
- "Refactor this code to use signals instead of direct references"
- "Debug why my player character falls through the floor sometimes"
- "Show me the full structure of my scene tree and explain the relationships"
- "Generate a script for enemy AI that follows the player"

## Available Resources and Commands

### Resource Endpoints:
- `godot://script/current` - The currently open script
- `godot://script/{path}` - Any script by path (NEW)
- `godot://scene/current` - The currently open scene
- `godot://scene/tree` - Complete scene tree hierarchy (NEW)
- `godot://project/info` - Project metadata and settings
- `godot://assets/{type}` - Assets of specific type (NEW)
- `godot://debug/log` - Debug output from editor (NEW)

### Command Categories:

#### Node Commands
- `get-scene-tree` - Returns the scene tree structure
- `get-node-properties` - Gets properties of a specific node
- `create-node` - Creates a new node
- `delete-node` - Deletes a node
- `modify-node` - Updates node properties

#### Script Commands
- `list-project-scripts` - Lists all scripts in the project
- `read-script` - Reads a specific script
- `modify-script` - Updates script content
- `create-script` - Creates a new script
- `analyze-script` - Provides analysis of a script

#### Scene Commands
- `list-project-scenes` - Lists all scenes in the project
- `read-scene` - Reads scene structure
- `create-scene` - Creates a new scene
- `save-scene` - Saves current scene

#### Project Commands
- `get-project-settings` - Gets project settings
- `list-project-resources` - Lists project resources

#### Editor Commands
- `get-editor-state` - Gets current editor state
- `run-project` - Runs the project
- `stop-project` - Stops the running project

#### Enhanced Commands (NEW)
- `get_full_scene_tree` - Gets complete hierarchical scene structure
- `get_debug_output` - Retrieves debug logs from editor
- `update_node_transform` - Updates node position, rotation, and scale
- `list_assets_by_type` - Lists project assets by type
- `ai_generate_script` - Generates script templates from descriptions

## Troubleshooting

### Connection Issues
- Ensure the plugin is enabled in Godot's Project Settings
- Check the Godot console for any error messages
- Verify the server is running when Claude Desktop launches it

### Plugin Not Working
- Reload Godot project after any configuration changes
- Check for error messages in the Godot console
- Make sure all paths in your Claude Desktop config are absolute and correct

## Adding the Plugin to Your Own Godot Project

If you want to use the MCP plugin in your own Godot project:

1. Copy the `addons/godot_mcp` folder to your Godot project's `addons` directory
2. Open your project in Godot
3. Go to Project > Project Settings > Plugins
4. Enable the "Godot MCP" plugin

## New Files Added in This Fork

This fork adds several new files to the original project:

- `server/src/resources/asset_resources.ts` - Asset querying functionality
- `server/src/resources/debug_resources.ts` - Debug output access
- `server/src/tools/ai_script_tools.ts` - AI script generation
- `addons/godot_mcp/mcp_enhanced_commands.gd` - Enhanced command processor
- `addons/godot_mcp/mcp_script_resource_commands.gd` - Script resource processor
- `addons/godot_mcp/mcp_asset_commands.gd` - Asset commands processor

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request to the [GitHub repository](https://github.com/waefrebeorn/Godot-MCP).

## Documentation

For more detailed information, check the documentation in the `docs` folder:

- [Getting Started](docs/getting-started.md)
- [Installation Guide](docs/installation-guide.md)
- [Command Reference](docs/command-reference.md)
- [Architecture](docs/architecture.md)
- [Enhanced Features Guide](docs/enhanced-features.md) (NEW)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## License

This project is licensed under the **Waefrebeorn Umbrella License v3.0**.
See the [LICENSE](LICENSE) file for the full license text.

The Waefrebeorn Umbrella License is a custom source-available license.
It is not OSI-approved and not FSF-approved.
