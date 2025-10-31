# Installing semantic-search

## Prerequisites

- Debian-based Linux distribution (Ubuntu, Debian, Linux Mint, etc.)
- Python 3.8 or higher
- Internet connection

## Installation Methods

### Method 1: Install from Custom APT Repository (Recommended)

#### Step 1: Add the GPG Key

Download and add the repository GPG key to verify package signatures.

**Modern Method (Ubuntu 21.04+, Debian 11+):**

```bash
wget -qO- https://kimixbb.github.io/semantic-search-apt/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/semantic-search-keyring.gpg > /dev/null
```

**Legacy Method (Older Systems):**

If you're on an older Ubuntu/Debian version, use:

```bash
wget -qO- https://kimixbb.github.io/semantic-search-apt/public.key | sudo apt-key add -
```

Note: You may see a warning that `apt-key is deprecated`. This is expected on modern systems - use the modern method above instead.

#### Step 2: Add the Repository

Add the APT repository to your sources.

**If you used the Modern Method (with signed-by):**

```bash
echo "deb [signed-by=/usr/share/keyrings/semantic-search-keyring.gpg] https://kimixbb.github.io/semantic-search-apt stable main" | sudo tee /etc/apt/sources.list.d/semantic-search.list
```

**If you used the Legacy Method (with apt-key):**

```bash
echo "deb https://kimixbb.github.io/semantic-search-apt stable main" | sudo tee /etc/apt/sources.list.d/semantic-search.list
```

**Important:** The entire `deb` line must be on ONE single line with no line breaks. Don't split the URL across multiple lines or you'll get a "Malformed entry" error.

#### Step 3: Update and Install

```bash
sudo apt update
sudo apt install semantic-search
```

### Method 2: Install from .deb File

Download the `.deb` file directly and install:

```bash
# Download the package
wget https://kimixbb.github.io/semantic-search-apt/pool/main/semantic-search_1.0.0_all.deb

# Install it
sudo dpkg -i semantic-search_1.0.0_all.deb

# Fix any dependency issues
sudo apt-get install -f
```

## Post-Installation Setup

### Configure API Key

The application requires a DeepSeek API key to function. Get your API key from [https://platform.deepseek.com/api_keys](https://platform.deepseek.com/api_keys)

Add the following to your `~/.bashrc`, `~/.zshrc`, or shell configuration file:

```bash
export DEEPSEEK_API_KEY="your-api-key-here"
```

Then reload your shell configuration:

```bash
source ~/.bashrc  # or source ~/.zshrc
```

Or set it temporarily for the current session:

```bash
export DEEPSEEK_API_KEY="your-api-key-here"
```

## Usage

Once installed, run the application with:

```bash
semantic-search /path/to/your/file.txt
```

### Key Bindings

- `/` - Initiate semantic search (powered by DeepSeek)
- `n` / `l` / `→` - Jump to next match
- `N` / `h` / `←` - Jump to previous match
- `r` - Cycle relevance level (STRICT → NORMAL → LOOSE)
- `Enter` - Re-run search with current relevance level
- `c` - Clear search highlighting and query
- `j` / `↓` - Scroll down one line
- `k` / `↑` - Scroll up one line
- `Page Down` - Scroll down one page
- `Page Up` - Scroll up one page
- `Ctrl-D` - Scroll down half page
- `Ctrl-U` - Scroll up half page
- `Home` - Jump to start of file
- `End` - Jump to end of file
- `q` / `ESC` - Quit (or clear search if active)

## Updating

To update to the latest version:

```bash
sudo apt update
sudo apt upgrade semantic-search
```

## Uninstalling

To remove the package:

```bash
sudo apt remove semantic-search
```

To completely purge all configuration:

```bash
sudo apt purge semantic-search
```

## Troubleshooting

### "Malformed entry" error when running apt update

This means your sources.list file has a line break in the middle of the `deb` entry.

**Fix:**
```bash
sudo rm /etc/apt/sources.list.d/semantic-search.list
echo "deb [signed-by=/usr/share/keyrings/semantic-search-keyring.gpg] https://kimixbb.github.io/semantic-search-apt stable main" | sudo tee /etc/apt/sources.list.d/semantic-search.list
sudo apt update
```

Make sure the entire `deb` line is on ONE single line with no line breaks.

### "Unable to locate package semantic-search"

The repository files aren't accessible. Check:

1. **GitHub Pages is deployed:** Visit https://kimixbb.github.io/semantic-search-apt/dists/stable/Release in your browser. If you get 404, the repository isn't deployed yet.

2. **Test file accessibility:**
   ```bash
   curl -I https://kimixbb.github.io/semantic-search-apt/dists/stable/Release
   ```
   Should return `HTTP/2 200`.

3. **Verify sources.list entry:**
   ```bash
   cat /etc/apt/sources.list.d/semantic-search.list
   ```
   Should be one line matching the format above.

### "DEEPSEEK_API_KEY environment variable not set"

Make sure you've exported the API key as shown in the Post-Installation Setup section.

### "Connection Error: Could not reach DeepSeek API"

- Check your internet connection
- Verify your API key is valid
- Check if you have any firewall blocking the connection

### "401 - Authentication Failed: Invalid API key"

Your API key is incorrect or expired. Get a new one from [https://platform.deepseek.com/api_keys](https://platform.deepseek.com/api_keys)

### "402 - Insufficient Balance"

Your DeepSeek account has insufficient balance. Add credits to your account at [https://platform.deepseek.com](https://platform.deepseek.com)

## Support

For issues, bugs, or feature requests, please visit:
- GitHub: https://github.com/Kimixbb/semantic_search

