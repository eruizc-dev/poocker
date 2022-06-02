# Notes

Here's my project thoughts as I develop them

### Hacks

Cool hacks I've learned from doing this project

#### Reuse code comments as help command

Writing a comment after each function like `#HELP description` and using sed to
generate the help message like so:

```sh
sed -n "s/^.*#HELP\\s//p;" < "$1"
```

This way your comments serve both as internal and external documentation, and
because they're physically closer the description from the implementation it's
harder to forget to update it after a modification.

#### Display help if no argument provided

A simple one liner

```sh
[[ -z "${1-}" ]] && bocker_help "$0"
```

#### Argument parsing

List all valid commands and use that to autocomplete the function name to be
invoked, in this case using `$1~

```sh
case $1 in
	pull|init|rm|images|ps|run|exec|logs|commit) bocker_"$1" "${@:2}" ;;
	*) bocker_help "$0" ;;
esac
```
