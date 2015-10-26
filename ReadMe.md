# Hello VS Code with TypeScript and Node

## Prerequisites

1. Install Node.js:
	- https://nodejs.org/en
	
2. Install Gulp and TypeScript packages *globally*.
	- Open a terminal and execute the following:	
	```
	npm install gulp typescript -g
	```

## Steps

1. Create a project folder and open it with VS Code
	- `cd` into the folder from Terminal and execute:
	```shell
	code .
	```
	
2. Initialize the `package.json` file.
	```shell
	npm init
	```
	- For the main entry point specify: `dest/index.js`
	- Respond to each prompt, then type `yes` to create the file.

3. Add the `gulp-tsc` package *locally*.
	```shell
	npm install --save-dev gulp gulp-tsc
	```
	- Creates `gulp` and `gulp-tsc` folders inside a `node_modules` folder.
	- Writes dev dependencies to the packages.json file.
	
4. Create a `gulpfile.js` file at the project root.
	- Copy the following code into the file:
	```js
	var gulp = require('gulp');
	var tsc = require('gulp-tsc');
	
	gulp.task('tsc-compile', function(){
	gulp.src(['src/**/*.ts'])
		.pipe(tsc())
		.pipe(gulp.dest('dest/'))
	});
	
	gulp.task('tsc-watch', function () {
	gulp.watch('src/**/*.ts', ['tsc-compile']);
	});
	```
	- The `tsc-compile` task transpiles .ts files into .js files
	- The `tsc-watch` task monitors .ts files and executes `tsc-compile` task when a change is detected.

5. Configure the Task Runner in VS Code.
	- Press **Cmd-Shft-P**, then type *'Config'* and click *'Configure Task Runner'*
	- Once the `tasks.json` file is created, replace the content with the following:
	
	```json
	{
		"version": "0.1.0",
		"command": "gulp",
		"isShellCommand": true,
		"args": [
			"--no-color"
		],
		"tasks": [
			{
				"taskName": "tsc-compile",
				"isBuildCommand": true,
				"showOutput": "always"
			},
			{
				"taskName": "tsc-watch",
				"isBuildCommand": true,
				"showOutput": "silent"
			}
		]
	}
	```	

6. Create an `src` folder and add an `index.ts` file to it.
	- Add the following content to the file:
	```js
	class Startup {
		public static main(): number {
			console.log('Hello World');
			return 0;
		}
	}
	Startup.main();
	```
	- Press **Cmd-Shft_B** to execute the 'tsc-compile' task.
	- An `index.js` file should appear in a `dest` folder.
	- Run the `tsc-watch` task, then change the message in `index.ts` to `Hello TypeScript`.
	- Saving the file will then result in `index.js` being updated.
	
7. Run the app.
	- From a terminal window execute node, passing dest/index.js
	
8. Debug the app.
	- Click the Debug icon in the sidebar, then click the Configure icon to create a launch.json file
	- Set a breakpoint in dest/index.js and press F5 to start the debugger.
