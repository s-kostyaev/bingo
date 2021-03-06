# bingo

bingo is a [Go](https://golang.org) language server that speaks
[Language Server Protocol](https://github.com/Microsoft/language-server-protocol).

This project was largely inspired by [go-langserver](https://github.com/sourcegraph/go-langserver),
but bingo more simpler, more faster, more smarter!

## Feature
bingo will support editor features as follow:

- [x] textDocument/hover
- [x] textDocument/definition
- [x] textDocument/xdefinition
- [x] textDocument/typeDefinition
- [x] textDocument/references
- [x] textDocument/implementation
- [x] textDocument/formatting
- [x] textDocument/rangeFormatting
- [x] textDocument/documentSymbol
- [x] textDocument/completion
- [x] textDocument/signatureHelp
- [x] textDocument/publishDiagnostics
- [x] textDocument/rename
- [ ] textDocument/codeAction
- [ ] textDocument/codeLens
- [x] workspace/symbol
- [x] workspace/xreferences

Differences between go-langserver, bingo, golsp.

- [go-langserver](https://github.com/sourcegraph/go-langserver)

> go-langserver is designed for online code reading such as github.com.

- [bingo](https://github.com/saibing/bingo)

> bingo is designed for offline editors such as vscode, vim, it focuses on code editing.

- [golsp](https://github.com/golang/tools/blob/master/cmd/golsp/main.go)

> golsp is an official language server,  and it is currently in early development.

## Install

bingo is a go module project, so you need install [Go 1.11 or above](https://golang.google.cn/dl/),
to build and install the `bingo`, please run

```bash
git clone https://github.com/saibing/bingo.git
cd bingo
go build
```

## Usage

### [vscode-go](https://github.com/Microsoft/vscode-go)

vscode's settings:

```json
{
    "go.useLanguageServer": true,

    "go.alternateTools": {
        "go-langserver": "bingo"
    },

    "go.languageServerFlags": ["--pprof", ":6060"],

    "go.languageServerExperimentalFeatures": {
        "format": true,
        "autoComplete": true
    }
}
```

### [LanguageClient-neovim](https://github.com/autozimu/LanguageClient-neovim)

neovim's settings:

```vim
let g:LanguageClient_rootMarkers = {
        \ 'go': ['.git', 'go.mod'],
        \ }

let g:LanguageClient_serverCommands = {
    \ 'go': ['bingo', '--mode', 'stdio', '--logfile', '/tmp/lspserver.log','--trace', '--pprof', ':6060'],
    \ }

```

## Note

bingo will create a global cache on startup, this will take some time.

If your disk io performance is very poor, you can get a good experience on hover, go to definition, find references by enable the -use-global-cache flag. 

But this will lead to miss some result for them, because currently bingo only rebuild the global cache when go.mod changes.

So the -use-global-cache flag is great for reading a large go language project's code, you will have very fast hover, find references, workspace symbol search etc.

## FAQ

- Please keep 'go build' or 'go list' command work ok

> If they have some errors when they execute, these errors may affect the accuracy of the bingo's results.
