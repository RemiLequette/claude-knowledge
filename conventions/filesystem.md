# Filesystem MCP Convention

## Rule
- **Read operations** → use `filesystem` MCP
- **Write operations** → use `edit-file-lines` MCP

## Rationale
Separation of concerns between read and write access.
Reduces risk of unintended modifications during read-only tasks.

`filesystem` reads raw text directly — faster and lower token consumption.
`edit-file-lines` provides robustness and efficiency for write operations (streaming, retry, verification, backup).

## Tools
### filesystem (read)
list_directory, read_file, read_text_file, read_multiple_files, get_file_info, directory_tree, search_files

### edit-file-lines (write)
fast_write_file, fast_large_write_file, fast_edit_block, fast_edit_multiple_blocks, fast_delete_file, fast_move_file
