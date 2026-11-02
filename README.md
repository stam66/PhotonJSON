[![Donate](https://img.shields.io/badge/Donate-QvaPay-green.svg)](https://qvapay.com/payme/ferruslogic?r_id=PhotonJSON&msg=Donate%20to%20Ferruslogic)

# PhotonJSON: JSON library for LiveCode language
[Leer en Español](LEEME.md)

> ### About this fork
>
> This fork is upstream [DTByte-Ltd/PhotonJSON](https://github.com/DTByte-Ltd/PhotonJSON) plus five
> fixes that have been submitted upstream as pull requests and are not yet merged. `main` has all of
> them together; each also lives on its own `fix/*` branch, which is what the pull request points at.
> Once upstream has merged them this note goes away and the fork tracks upstream again.
>
> | PR | Fix |
> |----|-----|
> | [#9](https://github.com/DTByte-Ltd/PhotonJSON/pull/9) | `JSONStringify` escapes backslashes (`\` is written as `\\`); `minifyJSON` no longer re-escapes. |
> | [#10](https://github.com/DTByte-Ltd/PhotonJSON/pull/10) | `JSONParser` decodes escapes in one pass by code point (no more `\\` becoming a space, no mis-read of the text an escape produces, surrogate pairs handled) and accepts UTF-8 as bytes, as text, or as text read with `url "file:"`. |
> | [#11](https://github.com/DTByte-Ltd/PhotonJSON/pull/11) | An empty string is written as `""` and a bare `null` reads back as empty; a quoted `"null"` stays a string. |
> | [#12](https://github.com/DTByte-Ltd/PhotonJSON/pull/12) | Text outside ASCII is written as UTF-8 instead of byte escapes by Mac Roman code; only control characters are escaped. |
> | [#13](https://github.com/DTByte-Ltd/PhotonJSON/pull/13) | Only a canonical number is written bare (`"3.10"`, `"007"`, `"1e5"` stay strings); `1e-5` parses as one value. |
>
> Each fix has a test stack in `testing/`. Run one headless with `<engine> -ui testing/<file>.livecodescript`,
> or load it in the IDE and call the command named in its header.

[LiveCode](https://livecode.com/) script library for working with JSON, written in livecode-script and without the use of external.

In this library ideas converge from many developers who created solutions like this in [LiveCode](https://livecode.com/) and in other programming languages. Although there are several libraries for working with JSON in [LiveCode](https://livecode.com/). We it a personal challenge to create our own version for which we took as a basis the great work done by Bob Hall in the [FastJSON](https://github.com/bhall2001/fastjson) library. We needed a library like [FastJSON](https://github.com/bhall2001/fastjson) and with the speed of Mount Goulding's [mergJSON](https://github.com/montegoulding/mergJSON). So we started writing PhotonJSON using FastJSON's ideas and code as a base, although in some cases we completely rewrote the algorithms.



## PhotonJSON improvements.

In PhotonJSON, a certain degree of optimization was achieved in the processes of analyzing a JSON. Therefore, the library has a performance very close to that obtained in mergJSON. Not forgetting that the latter makes use of an external that processes at a lower level than LiveCode and therefore is a little faster. These are some of the improvements we found in PhotonJSON.
1. Convert a JSON to an LC Array in a less time equal to or very close to that of mergJSON.
2. When converting an LC Array to JSON you can specify whether the JSON is beautifully formatted.
3. Added a nice formatting function and another to minify existing JSON.



## How to use PhotonJSON

To use PhotonJSON in your desktop or mobile applications you just have to load the library

```
start using stack "PhotonJSON"
```

If you are going to use PhotonJSON in your server application, you must create a plain text file with the extension .lc and copy the script from the PhotonJSON stack to this file without including the first line of it ("PhotonJSON" script).

```
<? lc ... the script of stack"PhotonJSON" ...?>
```

We already have PhotonJSON integrated into our project. So, we can access all the functions and properties of it.



> **NOTE**
> *Before continuing, let's clarify that in LiveCode if two libraries have a function with the same name. If this function is called from any other side of the code, the one from the last library that was called will be executed, that is, the one that is first in the message path.*



PhotonJSON has 5 functions and a public property that is, they can be accessed from another script. It also integrates 4 functions for compatibility with projects that use other libraries and want to start using this one. Please note the above note.

| Name          | Type     | Parameter                                                    | Returns           | Description                                 |
| :------------ | -------- | ------------------------------------------------------------ | ----------------- | ------------------------------------------- |
| validateJSON  | function | UTF-8 JSON string                                            | Boolean           | Validate if a string is a valid JSON.       |
| minifyJSON    | function | UTF-8 JSON string                                            | UTF-8 JSON string | Remove unnecessary spaces from JSON string. |
| beautifyJSON  | function | J UTF-8 JSON string                                          | UTF-8 JSON string | JSON string formatted in a more visually pleasing way. |
| JSONStringify | function | LC Array, if the type of the JSON elements is forced and if it is formatted in a beautiful way | UTF-8 JSON string | Gets the JSON string from an LC Array.      |
| JSONParser    | function | UTF-8 JSON string                                            | LC Array          | Gets the LC Array of a JSON string.         |

These are the four functions that are optionally included for PhotonJSON compatibility with projects that use mergeJSON or FastJSON. They expect the same parameters as in their original versions and in the same order.

```
ArrayToJSON(), JsonToArray(), arrayFromJson(), and jsonFromArray().
```

If you don't want PhotonJSON to overwrite the previous functions, just comment the code for it in the PhotonJSON library.


> [!IMPORTANT]
>**Why don't we use these names for the library and use `JSONStringify` and `JSONParser` as in the HTML5 API.**
> 
>*Since we created this library to be used in a plugin that will be integrated with the LiveCode IDE and as we clarify in the note. When a function is called and it is in two libraries, the first one in the path will take precedence over the others. So in order not to interfere with other projects where you don't want to use this library, we decided to use this naming convention and not include the others.*



### Copyright (C)  2020  FerrusLogic
