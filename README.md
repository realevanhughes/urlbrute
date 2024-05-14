# urlbrute
This is a command line tool for finding possible paths of a given URL using either word list, random or common paths.

The code is designed to take full advantage of the hardware available as it has the ability to run in multi-threaded mode.

The main wordlist can be edited in a standard text editor and is named "wordlist.txt".

However, modifying the wordlist for multi-threaded mode is slightly more difficult as it contains seperate wordlists for each letter of the alphabet (eg. "wordlist - a.txt" for the letter a).

## Requirements:
- requests (python module)
- threading (python module)

## Useage:

| Argument | Expanded argument | Details | Default |
| -------- | ----------------- | ------- | ------- |
| -h | --help | Displays help dialouge | n |
| -C | --common_mode | A pre-defined list of common URL paths are tried, path of file can be specified | n/common paths.txt |
| -R | --rand_mode | A random string will be tried as a path, number of attempts must be specified | n |
| -D | --dict_mode | Every word in the English dictionary will be tried as a path, path of file can be specified | n/wordlist.txt |
| -t | --multi_threading | Enables the multi-threading, number of threads must be specified if argument is used | n/26
| -g | --guided | Enables guided mode which is a menu with extra information about this tool | n |
| -u | --url | This is the root URL that will be used for the testing | - |
| -v | --verbose_output | Debug info will be given including thread info | n |
| -w | --wait | The scheduled delay between attempts | 0 |
| -e | --exclude | It will specify the response type that will be counted as a miss | 404,403 |

## Examples:
This example will try common paths on the site w3.org, with no wait time between attempts.
```
python urlbrute.py -u "https://w3.org" -C y -w 0
```
The output looks like this:
```
------------------------------RESULTS------------------------------
There were 9 results:

https://w3.org/about returned <Response [200]>
https://w3.org/contact returned <Response [200]>
https://w3.org/info returned <Response [200]>
https://w3.org/robots.txt returned <Response [200]>
https://w3.org/home returned <Response [300]>
https://w3.org/account returned <Response [200]>
https://w3.org/search returned <Response [200]>
https://w3.org/help returned <Response [200]>
https://w3.org/support returned <Response [200]>
-------------------------------------------------------------------
```
However, this example will try all words in the English dictionary as paths on the site google.com, with a wait time of 1 second.
```
python urlbrute.py -u "https://google.com" -D y -w 1
```
The output looks like this:
```
Took too long, I am lazy.
```
This example will try all words in the English dictionary as paths on the site youtube.com, with no wait time and 26 threads (the only available number of threads for this mode).
```
python urlbrute.py -u "https://youtube.com" -D y -w 0 -t 26
```
This was significantly quicker and outputed:
