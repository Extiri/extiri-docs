# Get snippets

```http://127.0.0.1:1300/v1/snippets/?key=<key>&query=<search query>&language=<language>&tag=<tag id>&group=<group id>```

Method: `GET`

This endpoint will return snippets stored in CodeMenu.

## Parameters
- key (optional, default: none) - user-specified protection key.
- query (optional, default: none) - server will return snippets which codes, titles or descriptions contain specified query. If absent, returns all snippets.
- language (optional, default: none) - server will return snippets in specified language. If absent, returns all snippets.
- tag (optional, default: none) - server will return snippets with tag with specified id. If absent, returns all snippets.
- group (optional, default: none) - server will return snippets in group with specified id. If absent, returns all snippets, returns snippets in specified group otherwise.
## Success response

- array of snippets:
  - id (string)
  - title (string)
  - description (string)
  - code (string)
  - language (string)
  - group (string, optional) - id of the group in which the snippet is
  - abbreviation (string)
  - tags (string array) - array of tag id's
  - placeholders
    - key - placeholder
    - value - placeholder action (see Placeholders and Example for explanation)


!!! note "Placeholders"
    Placeholder actions provide a way to make placeholders with special values. At this moment, one action is available (shell). When the value is "none", then placeholder is simply replaced with some value. When the value is "shell"then it is a shell placeholder. In such case, the placeholder should be replaced with the standard output of the command executed in a bash shell.




## Example

Request: 
```http://localhost:1300/v1/snippets```

Response:
```json
[
  {
    "id": "B6F50935-C7C8-4024-AEBE-588D76CA847E",
    "title": "Some example",
    "language": "prompt",
    "description": "A prompt, that is an example.",
    "placeholders": {},
    "abbreviation": "",
    "tags": [
      "1E126396-D086-4B00-96B7-C2CFE346F90A"
    ],
    "placeholders": {
      "directory": {
        "Shell": {
          "_0": "ls"
        }
      },
      "name": {
        "None": {}
      }
    },
    "code": "Hi! How are you? I'm @\__name__@. Here are some files @\__directory__@."
  },
  {
    "abbreviation": "nwd",
    "tags": [],
    "language": "swift",
    "placeholders": {},
    "code": "func NWD(a: Int, b: Int) -> Int {\n  var a = a\n  var b = b\n  \n  while a != b {\n    if a > b {\n      a -= b\n    } else {\n      b -= a\n    }\n  }\n  \n  return a\n}",
    "id": "EE7E3291-F559-4834-9477-BF28DE3F4E9E",
    "title": " Function to Find the Greatest Common Divisor (GCD) of Two Integers",
    "description": " This function, named NWD, takes two integer arguments, `a` and `b`. It returns the greatest integer that divides both `a` and `b` without leaving a remainder, also known as the greatest common divisor (GCD). The function achieves this by repeatedly reducing the larger argument by the smaller one until they become equal. The process is carried out in a `while` loop, where the larger argument is updated by subtracting the smaller one, and the function eventually returns the final value of `a`."
  }
]
```