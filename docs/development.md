## Development

All contributions are welcome. Some options to support the project includes,

* Add new features to the project
* Improve the docs
* Add new gorf apps that others can reuse, every new apps shoupld reside inside a repo for easy maintenance, 
request for individual repo creation in discussions.
* suggest more ideas


Recommended way is to use the go mode edit to replace deps with local dev version

```bash
go mod edit -replace github.com/go-gorf/auth=../auth
```
Or

```
replace github.com/go-gorf/gorf => ../gorf
replace github.com/go-gorf/auth => ../auth
```