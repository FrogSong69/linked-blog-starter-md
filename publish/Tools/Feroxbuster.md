feroxbuster is a fast, recursive content discovery tool written in Rust, designed to perform _forced browsing_ attacks. It brute-forces directories and files on web servers using wordlists to uncover hidden or unlinked resources that may contain sensitive information such as source code, credentials, or internal network details.


### Core Usage

At its core, feroxbuster takes a wordlist (a list of potential file or directory names) and appends each entry to the base URL to see if it exists.

Essential flags:
- `-u, --url <URL>` – Target URL (required unless using `--stdin`, etc.)
- `-w, --wordlist <FILE>` – Wordlist to use (can be local file or URL)
```bash
feroxbuster -u https://target.com -w /path/wordlist.txt
```
When feroxbuster gets a 200 OK (or other allowed status codes) for a URL and sees it looks like a directory (or when forced), it recursively scans that path too:
```http
https://example.com/admin/<wordlist_entries>
```
This continues until the recursion depth is reached or no new directories are found.

### Performance Architecture

Feroxbuster uses:

- Asynchronous Rust HTTP clients to handle many requests in parallel    
- Thread pools (50 by default) to control how many directories are scanned at once
- Optional rate limits to slow down the scan if needed

It’s built for both speed and stealth.

### Filtering and False Positive Protection

Feroxbuster has built-in filters to reduce noise and junk responses:

- Wildcard filtering: Detects and avoids servers that return 200 for every path
- Status code filters: Include or exclude specific response codes (e.g., ignore `403`, only include `200`)
- Size/word/line filters: Exclude responses that match common junk templates

### Smart Enhancements

If you use options like `--smart` or `--thorough`, feroxbuster:

- Collects discovered words from responses and dynamically adds them to the wordlist mid-scan
- Attempts likely backup file names for each discovered file (e.g. `index.php.bak`, `login.old`)
- Guesses additional file extensions like `.zip`, `.tar.gz`, `.bak`, etc.

This allows it to intelligently expand and adapt the scan for deeper coverage.

# Optional flag:

### File Extension Guessing

```bash
-x php,doc,docx,txt,conf,bak
```
`-x, --extensions <EXT>...` – Add file extensions to test
- Use `-x` when you want to type less
- Use `--extensions` when you want to be more explicit/clear, especially in scripts or shared commands

### Header and Cookie Customization

```bash
-H "Cookie: PHPSESSID=3a9fudjom19l0ua5i7vdmsjnc9"
```
- `-H, --headers <HEADER>` – Add custom headers
- `-b, --cookies <COOKIE>` – Add cookies
- `-a, --user-agent <AGENT>` – Set custom user-agent
- `-A, --random-agent` – Use a random user-agent

### Performance Tweaks

- `-t, --threads <NUM>` – Number of concurrent threads (default: 50)
- `--rate-limit <NUM>` – Requests per second limit
- `--timeout <SECONDS>` – Request timeout (default: 7s)

### Recursion Behavior

- `-n, --no-recursion` – Disable recursion    
- `-d, --depth <DEPTH>` – Max recursion depth (default: 4)
- `--force-recursion` – Recurse even when not a directory

### Response Filtering

- `-C, --filter-status <CODES>` – Exclude specific HTTP response codes (e.g., 404)
- `-S, --filter-size <SIZE>` – Filter by response size
- `-W, --filter-words <WORDS>` – Filter by word count


### Examples

1# 
```bash
feroxbuster -u http://<IP> \
    -b PHPSESSID=<COOKIE> \
    -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt \
    -x pdf,doc,docx,xls,xlsx,odt,php \
    -t 200 \
    -r
```
### What it's doing:

- `-u http://<IP>`: the target IP
- `-b PHPSESSID=...`: Sending a session cookie with every request (likely needed for auth)
- `-w ...`: Using a small but popular wordlist to guess paths
- `-x ...`: Appending extensions like `.pdf`, `.docx`, `.php`, etc. to each word
- `-t 200`: Running with 200 threads (very aggressive)
- `-r`: Allows **following redirects** (e.g. if a path redirects to login)
Try to find accessible documents, configs, or PHP pages behind an authenticated session at high speed.

2#

```bash
feroxbuster -u http://<IP>/daloradius/ \
    -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt \
    -t 200 \
    --depth 10 \
    --resume-from ferox-http_underpass_htb_daloradius_-1744478306.state
```

### What it's doing:

- `-u http://<IP>/daloradius/`: Starting scan in a specific subdirectory
- `-w ...`: Same small directory wordlist
- `-t 200`: High thread count for speed
- `--depth 10`: Allowing recursion up to 10 levels deep (default is 4)
- `--resume-from ...`: Resuming a previous interrupted scan from a saved state file
Deep scan a known subdirectory (`/daloradius/`) for additional hidden content, continuing from a previous long-running scan.

```
feroxbuster -u http://<IP> \
    -b PHPSESSID=<COOKIE> \
    -w /usr/share/seclists/Discovery/Web-Content/directory-list-2.3-small.txt \
    -t 200 \
    --depth 10 \
    -x pdf,doc,docx,xls,xlsx,odt
```

### What it's doing:

- `-u http://<IP>`: the target IP
- `-b ...`: Authenticated session
- `-w ...`: Brute-forcing using a solid wordlist
- `-t 200`: Fast, multi-threaded scan
- `--depth 10`: Deep recursion
- `-x ...`: Appending document file extensions to all paths

##### Difference from the first command:
- This one **omits** `.php` from the extensions
- This one **adds recursion depth** of 10
- It **doesn’t follow redirects** (no `-r`)
