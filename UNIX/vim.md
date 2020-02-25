# Vim

## Search and Replace

You can search and replace in vim using the `:s` (substitute) command.

s will substitute on the current line. For example, the following will only replace the word potatoe on the current line:
`:s/potatoe/tomatoe`

`%s` will substitute on all lines in the file. For example, the following will replace the first occurrence of potatoe on every line:
`:%s/potatoe/tomatoe`

### Flags

    g - Global (All occurrences)
    c - Ask for confirmation
    i - Case insensitive
    I - Case sensitive

`:%s/search_keyword/replace_with_this/g`

### Delimiters

When using the substitute command you can use delimiters other than `/`. This is useful if you're replace something like a URL with a lot of slashes in it. E.g:

`:%s_http://google.com/a/url_https://bing.com/b/url_g`
