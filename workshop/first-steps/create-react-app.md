
# Create React Application

As mentioned before, the GeoStyler UI is a React library. So before using GeoStyler, we should create
a basic React application that we then extend step by step.
To do so, just navigate into any folder you like and execute following command on the terminal:

<pre><xmp>npx create-react-app {{ site.data.vars.reactAppName }}</xmp></pre>

In this case _{{ site.data.vars.reactAppName }}_ is our application name and you can give it any name you like.
A folder with the same name should have been created within your current directory. With the help of
the command above, a basic React application should have been created within that directory. Also,
all dependencies and some neat developer tools such as hot-reloading were added as well. These tools
should facilitate the development process for us.

Now, move to the project directory with following command

<pre><xmp>cd {{ site.data.vars.reactAppName }}</xmp></pre>

and start the development server with

<pre><xmp>npm start</xmp></pre>

You should now be able to see the application on [http://localhost:3000](http://localhost:3000) in your browser.
It should look like this:

[![](./images/cra-startpage.png)](./images/cra-startpage.png)

Next, we remove the existing code, so we can start with an empty application. To do so, simply replace
the content of `src/App.js` with following code:

```js
import React from 'react';

function App() {
  return (
    <div></div>
  );
}

export default App;
```

In the next step, we will show how to install GeoStyler.
