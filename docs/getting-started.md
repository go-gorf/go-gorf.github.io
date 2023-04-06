# Getting Started

Firstly, Create a new main package with following code

``` go linenums="1" title="main.go" hl_lines="11 12"
package main

import (
	"log"

	"github.com/go-gorf/gorf"
	"github.com/go-gorf/gorf-contrib/auth"
)

func main() {
	r := BootstrapRouter()
	user := auth.User{}
	println(user.Email)
	err := r.Run()
	if err != nil {
		log.Fatal("Unable to create the gin server")
	} // listen and serve on 0.0.0.0:8080 (for windows "localhost:8080")
}

```

Next, Create a settings.go file in the main package with the following code snippet

``` go linenums="1" title="settings.go" hl_lines="11 12"
package main

import (
	"github.com/gin-gonic/gin"
	"github.com/go-gorf/gorf"
	"github.com/go-gorf/auth"
)

// add all the apps
var apps = []gorf.GorfApp{
	&auth.AuthApp,
}

func LoadSettings() {
	// jwt secret key
	Settings.SecretKey = "GOo8Rs8ht7qdxv6uUAjkQuopRGnql2zWJu08YleBx6pEv0cQ09a"
	Settings.DbConf = &SqliteBackend{
		"db.sqlite",
	}
}

// bootstrap server
func BootstrapRouter() *gin.Engine {
	gorf.Apps = append(apps)
	LoadSettings()
	gorf.InitializeDatabase()
	gorf.SetupApps()
	r := gin.Default()
	gorf.RegisterApps(r)
	return r
}
```