# markdown-html

Parse markdown and convert to html

## markdown specification

https://guides.github.com/features/mastering-markdown/

> In case of bold or italic we apply decoration to any characters between two nearest symbols in one block, with no care of spaces

## algorithm

We need a function which will convert markdown text to html
The text may contain blocks of several type, we can consider those blocks as a kind of tree:

- Code blocks (everything inside is a plain text)
- Lists
  - Headers, Qoutes
    - text decorations or parsers (bold, italic, link, image, inline code)

So we can split whole text into blocks by newline symbols, the result block kinds will be

- plain text
- header
- blockquote
- Code block start
- Code block end

When user types any new symbol we

1. Check whether it may have an impact (seek it in C/D list)
1. If not - continue, if yes - go to 3
1. Check if new symbol redefines block structure (f.e. \n), if yes go to 6
1. Check if new symbol redefines block type (f.e. adding # to the start), if yes go to 6
1. Check if new symbol redefines inline text decorations inside block, if yes go to 6
1. Apply changes and recalculate output.

#### C/D characters

- \_ (underscore)
- - (\* and \*\* consequenses)
- #
- 1
- .
- -
- >
- `
- \ (escape character)
- \n
- space
- [,]
- (,)
- h,t,t,p,:,/,f,t (for links)
