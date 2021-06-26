---
layout: default
css_id: code_snippets_bash
---

# Code Snippets (BASH)


## Using getopts

```
#!/bin/bash

usage() { echo "Usage: $0 [-w <width>] [-d <denom>] <numer>" 1>&2; }

main ()
{
  local opt_width="80"
  local opt_denom="100"

  while getopts ":d:w:" opt; do
    case "${opt}" in
      d) opt_denom="${OPTARG}";;
      w) opt_width="${OPTARG}";;
      *) echo "Unknown options \"${opt}\"" 1>&2; usage; return 1;;
    esac
  done
  shift $((OPTIND-1))

  if ! [ $# -gt 0 ]; then
    echo "Missing argument for <numer>" 1>&2
    return 1
  fi
  local arg_numer="${1}"; shift

  local fill_div=$((arg_numer * opt_width / opt_denom))

  local i=0
  for (( ; i < fill_div && i < opt_width; i++)); do
    echo -n -e "+"
  done
  for (( ; i < arg_width; i++)); do
    echo -n -e "-"
  done
}

main "${@}"

```