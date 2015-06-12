add bower.json

```
{
	"lib": {
		"name": "bower-rails generated lib assets",
		"dependencies": {
			"angular": "latest",
			"angular-route": "latest",
			"angular-animate": "latest",
			"angular-resource": "latest",
			"ng-token-auth": "latest",
			"angular-cookie": "latest"
		}
	},
	"vendor": {
		"name": "bower-rails generated vendor assets",
		"dependencies": {
		}
	}
}
```

```
rake bower:install
```
