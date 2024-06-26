## Scope
Directory BruteForce. Discover hidden or unlinked directories and files.


## Source
```
https://github.com/maurosoria/dirsearch.git
```

## Installation
```
git clone https://github.com/maurosoria/dirsearch.git
```
### Environment: Python

## Watch Video

 https://asciinema.org/a/380112

# ▶ Example Usage

## ▶Simple usage
``` 
python3 dirsearch.py -u https://target
```
```
python3 dirsearch -u http://url.com/ --skip-on-status=400,403,404,500
```
``` 
python3 dirsearch.py -e php,html,js -u https://target
```
``` 
python3 dirsearch.py -e php,html,js -u https://target -w /path/to/wordlist
```

## ▶Recursion
- Recursive brute-force is brute-forcing continuously the after of found directories. For example, if dirsearch finds ```admin/```, it will brute-force ```admin/*``` (```*``` is where it brute forces). To enable this feature, use -r (or --recursive) flag

``` 
python3 dirsearch.py -e php,html,js -u https://target -r
```

- You can set the max recursion depth with --max-recursion-depth, and status codes to recurse with --recursion-status

``` 
python3 dirsearch.py -e php,html,js -u https://target -r --max-recursion-depth 3 --recursion-status 200-399
```

- There are 2 more options: ```--force-recursive ``` and ``` --deep-recursive ```
     - Force recursive: Brute force recursively all found paths, not just paths end with ```/```
     - Deep recursive: Recursive brute-force all depths of a path (```a/b/c``` => add ```a/```, ```a/b/```)

     - If there are sub-directories that you do not want to brute-force recursively, use ``` --exclude-subdirs ```

``` 
python3 dirsearch.py -e php,html,js -u https://target -r --exclude-subdirs image/,media/,css/
```

## ▶Threads

The thread number (-t | --threads) reflects the number of separated brute force processes. And so the bigger the thread number is, the faster dirsearch runs. By default, the number of threads is 25, but you can increase it if you want to speed up the progress.

In spite of that, the speed still depends a lot on the response time of the server. And as a warning, we advise you to keep the threads number not too big because it can cause DoS (Denial of Service).

```
python3 dirsearch.py -e php,htm,js,bak,zip,tgz,txt -u https://target -t 20
```
## ▶Skip Status Code
```
python3 dirsearch -u http://url.com/ --skip-on-status=400,403,404,500
```
## ▶Prefixes / Suffixes

--prefixes: Add custom prefixes to all entries

``` 
python3 dirsearch.py -e php -u https://target --prefixes .,admin,_
```

## ▶Wordlist:

``` tools ```

## ▶Generated with prefixes:

``` 
tools
.tools
admintools
_tools
```

--suffixes: Add custom suffixes to all entries

``` 
python3 dirsearch.py -e php -u https://target --suffixes ~
```

## ▶Wordlist:
```
index.php
internal

```

## ▶Generated with suffixes:

```
index.php
internal
index.php~
internal~
```

## ▶Blacklist

Inside the ```db/``` folder, there are several "blacklist files". Paths in those files will be filtered from the scan result if they have the same status as mentioned in the filename.

Example: If you add ```admin.php``` into ```db/403_blacklist.txt```, whenever you do a scan that ```admin.php``` returns 403, it will be filtered from the result.

## ▶Filters

Use -i | --include-status and -x | --exclude-status to select allowed and not allowed response status-codes

For more advanced filters: --exclude-sizes, --exclude-texts, --exclude-regexps, --exclude-redirects and --exclude-response

``` 
python3 dirsearch.py -e php,html,js -u https://target --exclude-sizes 1B,243KB
```

``` 
python3 dirsearch.py -e php,html,js -u https://target --exclude-texts "403 Forbidden"
```

``` 
python3 dirsearch.py -e php,html,js -u https://target --exclude-regexps "^Error$"
```

``` 
python3 dirsearch.py -e php,html,js -u https://target --exclude-redirects "https://(.*).okta.com/*"
```

```
python3 dirsearch.py -e php,html,js -u https://target --exclude-response /error.html
```

## ▶Raw request

dirsearch allows you to import the raw request from a file. The content would be something looked like this:

``` GET /admin HTTP/1.1
Host: admin.example.com
Cache-Control: max-age=0
Accept: */*
```

Since there is no way for dirsearch to know what the URI scheme is, you need to set it using the --scheme flag. By default, dirsearch automatically detects the scheme.

## ▶Wordlist formats

Supported wordlist formats: uppercase, lowercase, capitalization

### Lowercase:

```
admin
index.html
```

### Uppercase:

```
ADMIN
INDEX.HTML
```

### Capital:
```
Admin
Index.html
```

## ▶Exclude extensions

Use -X | --exclude-extensions with an extension list will remove all paths in the wordlist that contains the given extensions

``` 
python3 dirsearch.py -u https://target -X jsp
```

### Wordlist:

```
admin.php
test.jsp
```

### After:
```
admin.php
```

## ▶Scan sub-directories

- From an URL, you can scan a list of sub-directories with --subdirs.

```
python3 dirsearch.py -e php,html,js -u https://target --subdirs /,admin/,folder/
```

## ▶Proxies

dirsearch supports SOCKS and HTTP proxy, with two options: a proxy server or a list of proxy servers.

```
python3 dirsearch.py -e php,html,js -u https://target --proxy 127.0.0.1:8080
```
```
python3 dirsearch.py -e php,html,js -u https://target --proxy socks5://10.10.0.1:8080
```
```
python3 dirsearch.py -e php,html,js -u https://target --proxylist proxyservers.txt
```

## ▶Reports

Supported report formats: simple, plain, json, xml, md, csv, html, sqlite

``` 
python3 dirsearch.py -e php -l URLs.txt --format plain -o report.txt 
```

``` 
python3 dirsearch.py -e php -u https://target --format html -o target.json
```

## ▶More example commands

```
cat urls.txt | python3 dirsearch.py --stdin
```
```
python3 dirsearch.py -u https://target --max-time 360
```
```
python3 dirsearch.py -u https://target --auth admin:pass --auth-type basic
```
```
python3 dirsearch.py -u https://target --header-list rate-limit-bypasses.txt
```

