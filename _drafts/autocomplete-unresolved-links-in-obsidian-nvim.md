---
layout: post
title: Autocomplete Unresolved Links In Obsidian.nvim
categories: Neovim
tags: [neovim, tutorial, completions, obsidian]
---

## Steps

**3 parts** 

- list of completions
- formatted list (source) that nvim-cmp understands
- register the source with nvim-cmp


## Make The List

Make a list for **nvim-cmp** to use for completions.


### Create the file

This looks through a directory, gets information, and returns a lua table with that information structured in a way that other things can use it. It'll be easy to transform into a source for nvim-cmp, but it can be used for other things too. It's a stand alone utility, so it can live in *utils/*.

Create *utils/wikilinks.lua* 


### Set Up The "Module"

To make it easy to grab all the individual functions, create a "module" in a lua table. 

```lua
local M = {}

return M
```


### Where Are The Files?

Call it what you want, but in [Obsidian](https://obsidian.md/) it's a "vault". This is meant to complement the completions that come with [Obsidian.nvim](https://github.com/obsidian-nvim/obsidian.nvim), so for this post, it's a "vault".

Where is the vault? The machine needs to know what directory to scan. We'll set it up in the file. There are ways to make this more flexible, and you can do that later, once this is all up and running.

```lua
local vault_path = vim.fn.expand("~/path/to/your/vault")
```


### Things To Skip

Some things don't need to be scanned. There shouldn't be any wikilinks in *.git/*, or in the templates directory. Also, files should be able to be skipped too.

Set the directories and files to ignore here.

```lua
local exclude_dirs = { ".git", ".obsidian", "Templates", "Images" }
local exclude_files = { ".nvim_wikilink_index.json" }
```


## Obsidian's Completions

[Obsidian.nvim](https://github.com/obsidian-nvim/obsidian.nvim) has completions for wikilinks. The limitation is that it suggests only files that already exist in your vault. 

[Obsidian](https://obsidian.md/) and [Foam in VSCode](https://marketplace.visualstudio.com/items?itemName=foam.foam-vscode) also suggest "unresolved links". These are things that've been linked to but don't have files yet. There's no need to create and manage all those files. Once a file is created, though, all the backlinks are there ready to go. These unresolved links work like tags with superpowers. 

Completions for current files already exist in an [Obsidian.nvim](https://github.com/obsidian-nvim/obsidian.nvim) vault. This walkthrough sets up completions for links that don't already have files. It can also be used to set up wikilink completions outside of [Obsidian.nvim](https://github.com/obsidian-nvim/obsidian.nvim) vaults for both files and unresolved links.


## Get The Filenames

First, we'll get a list of the current files in all the directories inside our `vault_path`. [Ripgrep](https://github.com/BurntSushi/ripgrep) is a good friend in this situation. The grep that comes with your computer works, but it's SLOW compared to [Ripgrep](https://github.com/BurntSushi/ripgrep). There are other fast grep utilities, too, no judgement. Their commands might be slightly different, though.

{% capture get_markdown_files_function %}
  ```lua
  local function get_markdown_files()
    local cmd = {
      "rg",
      "--files",
      "--iglob",
      "*.md",
      vault_path,
    }

    for _, dir in ipairs(exclude_dirs) do
    table.insert(cmd, "--glob")
    table.insert(cmd, "!" .. dir .. "/**")
    end

    for _, file in ipairs(exclude_files) do
    table.insert(cmd, "--glob")
    table.insert(cmd, "!" .. file)
    end

    return vim.fn.systemlist(cmd)
  end
  ```
  {: file="get_markdown_files()" }
{% endcapture %}

{% include collapsible_block.html content=get_markdown_files_function button_text="See the full function" %}

It's time to build the query. First grab all the markdown files in the *vault_path*. 

```lua
local function get_markdown_files()
  local cmd = {
    "rg",
    "--files",
    "--iglob",
    "*.md",
    vault_path,
  }
end
```

Now, add the directories to skip:

```lua
local function get_markdown_files()
  ...

  for _, dir in ipairs(exclude_dirs) do
    table.insert(cmd, "--glob")
    table.insert(cmd, "!" .. dir .. "/**")
  end
end

```

Next, add the files to skip:

```lua
local function get_markdown_files()
  ...

  for _, file in ipairs(exclude_files) do
    table.insert(cmd, "--glob")
    table.insert(cmd, "!" .. file)
  end
end

```

Now vim can run the full command:

```lua
local function get_markdown_files()
  ...

  return vim.fn.systemlist(cmd)
end
```


## Get All The Wikilinks In The Vault

It's time to walk through the files and grab all the wikilinks. Feed this function a file, it loops through each line and finds all the `[[wikilinks]]`

{% capture extract_links_from_lines_function %}
  ```lua
  local function extract_links_from_lines(lines)
    local links = {}

    for _, line in ipairs(lines) do
      for link in line:gmatch("%[%[([^%]|%]]+)") do
        link = link:match("^[^|]+") -- strip off alias if present

        table.insert(links, link)
      end
    end

    return links
  end
  ```
  {: file="extract_links_from_lines()" }
{% endcapture %}

{% include collapsible_block.html content=extract_links_from_lines_function button_text="See the full function" %}

Start with an empty list.

```lua
local function extract_links_from_lines(lines)
  local links = {}
end
```

Now, loop through each line and find the `[[wikilinks]]`. This matches the link syntax and also strips out the `|alias` after the link name, leaving you with only the link text inserted into the list.

```lua
local function extract_links_from_lines(lines)
  ...

  for _, line in ipairs(lines) do
    for link in line:gmatch("%[%[([^%]|%]]+)") do
      link = link:match("^[^|]+") -- strip off alias if present

      table.insert(links, link)
    end
  end
end
```

Return the links:

```lua
local function extract_links_from_lines(lines)
  ...

  return links
end
```

- Get a list of all the wikilinks in the vault
- Sort the wikilinks into sections
  - resolved: matches a filename
  - unresolved: all the rest (no file yet)
- Make a list of the links in each file
  - Lets us update the whole list of unresolved links on a per file basis
  - Update our list each time you save a file without scanning the whole vault


## Setup The Completion Source

- Set the filetype to markdown
- Set the trigger
- Set the matching pattern
- Format the list to work with nvim-cmp


## Add the completion source

- Only in the vault (.nvim.lua)
- Everywhere (nvim-cmp setup)
- Settings
  - register the source
  - formatting
  - add it to the sources
      

