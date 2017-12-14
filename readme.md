ionic start ioniccli-meteor-tabs tabs --cordova --no-link

add to package.json:
	"config": {
		"ionic_webpack": "./webpack.config.js"
	} to

copy out the standard webpack.config.js to root:
	cp node_modules/@ionic/app-scripts/config/webpack.config.js .

	need to update for Typescript modules, alias for Meteor server, and ability to import Meteor/Cordova plugins
	(compare original and modified for details)

update tsconfig.json with api folder:
	"include": [..., "api/**/*.ts"]
	"exclude": [..., "api/nodemodules", "api"]

update tsconfig with additional compiler options so we can load Meteor as external dependency -> specification for CommonJS instead of es2015:
	"compilerOptions": {
		"baseUrl": ".",
		"module": "commonjs",
		"paths": {
			"api/*": ["./api/server/*"]
		},
		"skipLibCheck": true,
		"stripInternal": true,
		"noImplicitAny": false,...
	}

npm install --save-dev typescript-extends
npm install --save-dev @types/meteor