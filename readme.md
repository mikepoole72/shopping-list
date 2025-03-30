# Setting Up a React and TypeScript Project with Webpack

## 1. Create a Project Folder

Create a folder, for example, in `C:\Development\repos`.

## 2. Open the Folder in VS 2022

- Open Visual Studio 2022 and select **Open a local folder**.
- In Solution Explorer, right-click and select **Open in Terminal**.
- If you need administrator privileges, open **Command Prompt as Administrator** separately and run:
  ```sh
  cd C:\Development\repos\MyNewFolder
  ```

## 3. Initialize the Project

Create a `package.json` file:
```sh
npm init -y
```

## 4. Install Dependencies

Install React, ReactDOM, and TypeScript:
```sh
npm install react react-dom
npm install typescript @types/react @types/react-dom
```

## 5. Configure TypeScript

Initialize a `tsconfig.json` file:
```sh
npx tsc --init
```

Example `tsconfig.json`:
```json
{
  "compilerOptions": {
    "target": "es5",
    "jsx": "react-jsx",
    "module": "ES6",
    "moduleResolution": "node",
    "allowJs": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "strict": true,
    "skipLibCheck": true
  }
}
```

## 6. Install Webpack and Loaders

Install Webpack and necessary dependencies:
```sh
npm install --save-dev webpack webpack-cli webpack-dev-server html-webpack-plugin ts-loader style-loader css-loader
```

## 7. Create Webpack Configuration

Create `webpack.config.js` in the root directory:
```js
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/index.tsx',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist'),
    },
    resolve: {
        extensions: ['.ts', '.tsx', '.js', '.json'],
    },
    module: {
        rules: [
            {
                test: /\.(ts|tsx)$/,
                use: 'ts-loader',
                exclude: /node_modules/,
            },
            {
                test: /\.js$/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env'],
                    },
                },
                exclude: /node_modules/,
            },
        ],
    },
    devtool: 'source-map',
    devServer: {
        static: {
            directory: path.join(__dirname, 'dist'),
        },
        port: 3000,
        hot: true,
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './public/index.html',
        }),
    ],
};
```

## 8. Set Up Project Structure

```
src/
  index.tsx
  App.tsx
public/
  index.html
tsconfig.json
webpack.config.js
package.json
```

### 8.1 Create `src/index.tsx`
```tsx
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';

const root = ReactDOM.createRoot(document.getElementById('root') as HTMLElement);

root.render(
    <React.StrictMode>
        <App />
    </React.StrictMode>
);
```

### 8.2 Create `src/App.tsx`
```tsx
import React from 'react';

const App: React.FC = () => {
    return (
        <div>
            <h1>Hello, React with TypeScript</h1>
        </div>
    );
};

export default App;
```

### 8.3 Create `public/index.html`
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>React App</title>
</head>
<body>
    <div id="root"></div> <!-- React will render here -->
</body>
</html>
```

## 9. Add Scripts to `package.json`

```json
"scripts": {
  "start": "webpack serve --open --mode development",
  "build": "webpack --mode production"
}
```

- `start`: Runs the development server.
- `build`: Bundles the app for production.

## 10. Run the App

Start the development server:
```sh
npm start
```

