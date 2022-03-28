# Pre-Requisites
-   .NET SDK
-   NodeJS LTS

# Create new .NET project

```bash
dotnet new webapp -o vuejs-dotnet-starter
cd vuejs-dotnet-starter
```

Delete unnecessary files

```
wwwroot/css
wwwroot/js
wwwroot/lib
Pages/Shared/**
Pages/_ViewStart.cshtml
Pages/Index.cshtml
Pages/Privacy.cshtml
```

# Create VueJS app

```bash
mkdir ClientApp
cd ClientApp
```

Create _package.json_

```json
{
  "name": "clientapp",
  "version": "1.0.0",
  "scripts": {  },
}
```

Install Vue dependencies

```bash
npm install vue
npm install -D @vue/cli-service vue-template-compiler
```

Add scripts to _package.json_

```json
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build"
```

Add _src/App.vue_

```jsx
<template>
  <div id="app">
     <h1>Welcome to VueJS</h1>
  </div>
</template>
<script>
    export default {
        name: 'App'
    }
</script>
```

Add _src/index.js_

```jsx
import Vue from 'vue'
import App from './App'

new Vue({
    render: h => h(App),
}).$mount('#app');
```

Add _public/index.html_

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>VueJS + .NET starter app</title>
</head>
<body>
    <noscript>
        <strong>Please enable JavaScript in your browser. </strong>
    </noscript>
    <div id="app"></div>
</body>
</html>
```

# Add linting

```bash
npm install -D eslint eslint-plugin-vue
```

Add _.eslintrc.json_

```json
{
    "root": true,
    "env": {
        "node": true
    },
    "extends": [
        "plugin:vue/essential",
        "eslint:recommended"
    ],
    "rules": {}
}
```

# Configure SPA

Fallback .NET to index page in program.cs

```jsx
app.MapFallbackToFile("index.html");
```

Add SPA proxy package

```bash
dotnet add package Microsoft.AspNetCore.SpaProxy --prerelease
```

Configure SPA in csproj file

```xml
<SpaRoot>ClientApp\\</SpaRoot>
<DefaultItemExcludes>$(DefaultItemExcludes);$(SpaRoot)node_modules\\**</DefaultItemExcludes>
<SpaProxyServerUrl><http://localhost:8080></SpaProxyServerUrl>
<SpaProxyLaunchCommand>npm run serve</SpaProxyLaunchCommand>
```

Add environment variable in _Properties/launchSettings.json_

```json
"ASPNETCORE_HOSTINGSTARTUPASSEMBLIES": "Microsoft.AspNetCore.SpaProxy"
```

# Configure project publish

Make sure ClientApp folder does not get published

```xml
<ItemGroup>
  <Content Remove="$(SpaRoot)**" />
  <None Remove="$(SpaRoot)**" />
  <None Include="$(SpaRoot)**" Exclude="$(SpaRoot)node_modules\\**" />
</ItemGroup>
```

Configure Publishing Target in csproj file