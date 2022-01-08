# Part 1 - Very basic setup

As of Webpack 4, a config file is not needed so let's see how we can create a build.

yarn init -y

yarn add webpack webpack-cli --dev

In the root level create a folder `/dist` with a file `index.html` inside and another folder `/src` in the root level and add a `index.js` file inside it. Your file structure should look like the following:

````
|- package.json
|- package-lock.json
|- /dist
    |- index.html
|- /src
    |- index.js```
````

In your `package.json`, replace `"main": "index.js",` with `"private": true` to prevent it from accidently publishing your package.

Your `dist/index.html` file should look like this:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Webpack</title>
    <script src="main.js"></script>
  </head>
  <body></body>
</html>
```

As a example, add a console log to your `./src/index.js`

```
const greetings = "Hello World";
console.log(greetings);
```

This is all that is needed for a very basic build. Now run `yarn webpack` and you can see a new, compiled file `main.js` to appear in `./dist`. The compiled file should look like the following:

```
console.log("Hello World");
```

---

# Part 2 - Adding a custom config file

In the root level, add a file called `webpack-config.js` and then add the following configs:

```
import path from "path";

export default {
  entry: "./src/index.js",
  output: {
    path: path.resolve(__dirname, "dist"),
    filename: "main.js",
  },
};
```

# Part 3 - Add script command

```
"build": "webpack --mode development"
```

# Part 4 - Add TypeScript

Install dependancies

```
yarn add typescript ts-loader ts-node --dev
```

Add a new file `tsconfig.json` to the root level of the project and add the following configs:

```
{
    "compilerOptions": {
      "target": "ESNEXT",
      "module": "commonjs",
      "strict": true, 
      "esModuleInterop": true, 
      "skipLibCheck": true,
      "forceConsistentCasingInFileNames": true,
      "resolveJsonModule": true
    }
  }
```

Then open your webpack-config and add the following below `output`

```
module: {
  rules: [
    {
      test: /\.tsx?$/,
      use: "ts-loader",
      exclude: /node_modules/,
    },
  ],
},
resolve: {
  extensions: [".tsx", ".ts", ".js"],
},
```

Replace the entry file extension in your webpack-config to:

```
entry: path.resolve(__dirname, "src/index.ts")
```