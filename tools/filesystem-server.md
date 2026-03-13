# Filesystem Server

The filesystem server provides AI-powered file access — reading, writing, editing, and semantic code search across your local projects.

## Tools

### Search

| Tool | Description |
|------|-------------|
| `search_semantic` | Search code by meaning using embeddings |
| `search_files` | Search by filename glob patterns |

### Read

| Tool | Description |
|------|-------------|
| `read_text_file` | Read text files with optional line ranges |
| `read_media_file` | Read binary files as base64 |
| `read_multiple_files` | Batch read multiple files |

### Write

| Tool | Description |
|------|-------------|
| `write_file` | Create or overwrite a file |
| `edit_file` | Make targeted edits to existing files |
| `create_directory` | Create directories |
| `move_file` | Move or rename files |

### Explore

| Tool | Description |
|------|-------------|
| `list_directory` | List files and directories |
| `list_directory_with_sizes` | List with file sizes |
| `directory_tree` | Recursive tree view |
| `get_file_info` | File metadata |
| `list_allowed_directories` | Show sandboxed directories |

### Dashboard

| Tool | Description |
|------|-------------|
| `open_dashboard` | Browser-based index management |

## Semantic Search

The filesystem server builds a semantic index of your code using tree-sitter for parsing and fastembed for embeddings. This lets you search by *meaning* — "where is authentication handled?" works even if the code never uses the word "authentication."

Indexes are built automatically by a background watcher. The first search in an unindexed repo may be slow while the index builds; subsequent searches use the cache.

## Security

All file operations are sandboxed to explicitly allowed directories configured at server startup. Path traversal is blocked by validation.
