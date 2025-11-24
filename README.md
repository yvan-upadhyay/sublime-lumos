# sublime-lumos

Sublime Text package for [LUMOS](https://lumos-lang.org) - Type-safe schema language for Solana development.

![Version](https://img.shields.io/badge/version-0.1.0-blue)
![Sublime Text](https://img.shields.io/badge/Sublime%20Text-4-orange)
![License](https://img.shields.io/badge/license-MIT%20%2F%20Apache--2.0-green)

---

## Features

- **Syntax Highlighting** - Full syntax support for `.lumos` files
- **LSP Integration** - Auto-completion, diagnostics, hover documentation via `lumos-lsp`
- **Snippets** - Quick scaffolding for structs, enums, and Solana accounts
- **Auto-Indentation** - Smart indentation for LUMOS syntax
- **Comment Toggling** - `Ctrl+/` (or `Cmd+/`) to toggle line/block comments

---

## Installation

### Method 1: Package Control (Recommended - When Published)

1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Run: `Package Control: Install Package`
3. Search for: `LUMOS`
4. Install

### Method 2: Manual Installation

#### macOS / Linux

```bash
cd ~/Library/Application\ Support/Sublime\ Text/Packages
# or on Linux: ~/.config/sublime-text/Packages
git clone https://github.com/getlumos/sublime-lumos.git LUMOS
```

#### Windows

```powershell
cd "%APPDATA%\Sublime Text\Packages"
git clone https://github.com/getlumos/sublime-lumos.git LUMOS
```

### Method 3: Git-based Installation (via Package Control)

1. Open Command Palette
2. Run: `Package Control: Add Repository`
3. Enter: `https://github.com/getlumos/sublime-lumos`
4. Run: `Package Control: Install Package`
5. Select: `sublime-lumos`

---

## LSP Integration

For full IDE features (auto-completion, diagnostics, hover, go-to-definition), you need:

### Prerequisites

1. **Install LSP package** (from Package Control):
   - Open Command Palette → `Package Control: Install Package` → `LSP`

2. **Install lumos-lsp server**:
   ```bash
   cargo install lumos-lsp
   ```

### Configuration

The package includes LSP configuration out-of-the-box. After installing the LSP package and `lumos-lsp` server, restart Sublime Text.

**Custom LSP Settings** (optional):

Go to: `Preferences` → `Package Settings` → `LSP` → `Servers` → `LSP-lumos`

```json
{
  "clients": {
    "lumos-lsp": {
      "command": ["lumos-lsp"],  // or full path: ["/path/to/lumos-lsp"]
      "enabled": true
    }
  }
}
```

### Verify LSP is Running

1. Open a `.lumos` file
2. Check the status bar (bottom-left) for `lumos-lsp` indicator
3. If green ✓ → LSP is working
4. If red ✗ → Check LSP logs: `Tools` → `LSP` → `Troubleshoot Server`

---

## Snippets

Type these triggers and press `Tab`:

| Trigger | Description | Output |
|---------|-------------|--------|
| `struct` | Basic struct | `struct Name { field: u64 }` |
| `enum` | Unit enum | `enum Name { Variant1, Variant2 }` |
| `enumtuple` | Tuple variant enum | `enum Name { Variant(u64, String) }` |
| `enumstruct` | Struct variant enum | `enum Name { Variant { field: u64 } }` |
| `account` | Solana account struct | `#[solana] #[account] struct AccountName { ... }` |
| `deprecated` | Deprecated field | `#[deprecated("message")] field: Type` |

**Example Workflow:**

1. Type `account` → Press `Tab`
2. Type account name → Press `Tab`
3. Type field name → Press `Tab`
4. Type field type → Done!

---

## Syntax Highlighting

LUMOS package provides rich syntax highlighting for:

- **Keywords**: `struct`, `enum`, `use`, `pub`, `type`, `const`
- **Primitive Types**: `u8`-`u128`, `i8`-`i128`, `f32`, `f64`, `bool`, `String`
- **Solana Types**: `PublicKey`, `Pubkey`, `Signature`, `Keypair`
- **Complex Types**: `Vec<T>`, `Option<T>`, arrays `[T]`
- **Attributes**: `#[solana]`, `#[account]`, `#[version]`, `#[deprecated]`
- **Comments**: Line (`//`) and block (`/* */`)
- **Operators**: `->`, `=>`, `::`, `<`, `>`
- **Numbers**: Decimal, hex (`0x`), binary (`0b`), octal (`0o`)

---

## Settings

Default settings are optimized for LUMOS development:

```json
{
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "trim_trailing_white_space_on_save": true,
  "ensure_newline_at_eof_on_save": true
}
```

**Override Settings:**

`Preferences` → `Settings - Syntax Specific` (when editing a `.lumos` file)

---

## Keybindings

| Shortcut | Action |
|----------|--------|
| `Ctrl+/` (or `Cmd+/`) | Toggle line comment |
| `Ctrl+Shift+/` | Toggle block comment |
| `Ctrl+Space` | Trigger auto-completion (LSP) |
| `Ctrl+Click` | Go to definition (LSP) |
| `Ctrl+K, Ctrl+I` | Show hover documentation (LSP) |

---

## Troubleshooting

### Syntax Highlighting Not Working

- Ensure file has `.lumos` extension
- Restart Sublime Text
- Check: `View` → `Syntax` → `LUMOS`

### LSP Not Working

1. Verify `lumos-lsp` is installed:
   ```bash
   which lumos-lsp  # Should show path
   lumos-lsp --version
   ```

2. Check LSP package is installed:
   - `Preferences` → `Package Control` → `List Packages` → Look for `LSP`

3. Check LSP logs:
   - `Tools` → `LSP` → `Toggle Log Panel`
   - Look for errors related to `lumos-lsp`

4. Restart LSP server:
   - Open Command Palette → `LSP: Restart Servers`

### Snippets Not Working

- Type the trigger word (e.g., `struct`)
- Press `Tab` (not `Enter`)
- Ensure cursor is in a `.lumos` file

---

## Example LUMOS File

```lumos
// NFT Metadata Account
#[solana]
#[account]
struct NftMetadata {
    mint: PublicKey,
    name: String,
    symbol: String,
    uri: String,
    royalty_percentage: u16,
}

// NFT State
enum NftState {
    Minted,
    Listed { price: u64 },
    Sold { buyer: PublicKey, price: u64 },
}
```

---

## Related Projects

- **[lumos](https://github.com/getlumos/lumos)** - Core compiler and CLI
- **[vscode-lumos](https://github.com/getlumos/vscode-lumos)** - VS Code extension
- **[intellij-lumos](https://github.com/getlumos/intellij-lumos)** - IntelliJ IDEA plugin
- **[nvim-lumos](https://github.com/getlumos/nvim-lumos)** - Neovim plugin
- **[lumos-mode](https://github.com/getlumos/lumos-mode)** - Emacs mode
- **[docs-lumos](https://github.com/getlumos/docs-lumos)** - Official documentation

---

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

**Development:**

- Test syntax changes: Edit `LUMOS.sublime-syntax` and reload Sublime Text
- Test snippets: Edit `.sublime-snippet` files in `snippets/`
- Report issues: [GitHub Issues](https://github.com/getlumos/sublime-lumos/issues)

---

## License

Dual-licensed under MIT OR Apache-2.0. See [LICENSE-MIT](LICENSE-MIT) and [LICENSE-APACHE](LICENSE-APACHE).

---

## Resources

- **Website**: https://lumos-lang.org
- **Documentation**: https://docs.lumos-lang.org
- **Repository**: https://github.com/getlumos/sublime-lumos
- **Issues**: https://github.com/getlumos/sublime-lumos/issues
- **LSP Server**: https://crates.io/crates/lumos-lsp

---

**Built with ❤️ by the LUMOS community**
