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

## ⚠️ bash_tool ne fonctionne pas pour les fichiers locaux
`bash_tool` s'exécute dans un container Linux isolé — il n'a **pas** accès
au filesystem Windows de l'utilisateur. Ne jamais l'utiliser pour lire,
écrire ou manipuler des fichiers locaux. Toujours utiliser `filesystem`
ou `edit-file-lines`.

## Stratégie quand un remplacement échoue (old_text non trouvé)
Ne pas essayer bash. À la place :
1. Utiliser `edit-file-lines:fast_read_file` avec `line_start` + `line_count`
   pour lire les lignes exactes autour de la zone à modifier
2. Copier le texte exact tel qu'il apparaît dans le fichier (encodage, espaces, apostrophes)
3. Réessayer `filesystem:edit_file` ou `fast_edit_block` avec la chaîne corrigée
