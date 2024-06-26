<div align="center">

![Kulala Logo](logo.svg)

# kulala.nvim

![Lua](https://img.shields.io/badge/Made%20with%20Lua-blueviolet.svg?style=for-the-badge&logo=lua)
![Project Status](https://img.shields.io/badge/Alpha%20Status-green?style=for-the-badge&logo=github)

[Requirements](#requirements) • [Install](#install) • [Usage](#usage) • [HTTP File Spec](https://kulala.mwco.app/#/http_file_spec)

<p></p>

A minimal REST-Client Interface for Neovim.

Kulala is swahili for "rest" or "relax".

It allows you to make HTTP requests from within Neovim.

<p></p>

</div>

## Requirements

- [Neovim](https://github.com/neovim/neovim) (tested with 0.10.0)
  - [Treesitter for HTTP](https://github.com/nvim-treesitter/nvim-treesitter?tab=readme-ov-file#supported-languages) (`:TSInstall http`)
- [cURL](https://curl.se/) (tested with 8.5.0)
- [jq](https://stedolan.github.io/jq/) (tested with 1.7)

### Optional requirements

To make things a lot easier,
you can put this lua snippet somewhere in your configuration:

```lua
vim.filetype.add({
  extension = {
    ['http'] = 'http',
  },
})
```

This will make Neovim recognize files
with the `.http` extension as HTTP files.

## Install

Via [lazy.nvim](https://github.com/folke/lazy.nvim):


### Simple configuration

```lua
require('lazy').setup({
  -- HTTP REST-Client Interface
  { 'mistweaverco/kulala.nvim' },
})
```

## Public methods

### `require('kulala').run()`

Run the current request.

## Usage

The syntax highlighting for HTTP files on GitHub is not perfect.

It shows errors where there are none.

`examples.http`

```http

# Make a request to the PokeAPI to get information about ditto
# Use HTTP/1.0 and the application/json content type as headers
GET https://pokeapi.co/api/v2/pokemon/ditto HTTP/1.0
accept: application/json

###

# Make a request to the Star Wars API to get information about all films
# Use a GraphQL query to get the title and episodeID of each film
# Use the application/json content type as the header and omit the HTTP version
# so it defaults to HTTP/1.1
GET https://swapi-graphql.netlify.app/.netlify/functions/index
accept: application/json

< ./starwars.graphql

###

POST https://swapi-graphql.netlify.app/.netlify/functions/index
accept: application/json
content-type: application/json

{
  "query": "{ allFilms { films { title } } }",
  "variables": {}
}

###
```

`starwars.graphql`

```graphql
query {
  allFilms {
    films {
      title
      episodeID
    }
  }
}
```

Place the cursor on any item
in the `examples.http` and
run `:lua require('kulala').run()`.

