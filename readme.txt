tailwindcss + react styled component

 yarn add tailwindcss tailwind.macro@next styled-components babel-plugin-macros postcss-cli autoprefixer




 npx tailwind init    ->tailwind.config.js  -> scr 폴더로 이동

 scr/tailwind.css 파일 만들기

@tailwind base;

@tailwind components;

@tailwind utilities;





 babel-plugin-macros.config.js 파일 만들기  //루트 폴더

module.exports = {
  tailwind: {
    plugins: ["macros"],
    config: "./src/tailwind.config.js",
    format: "auto"
  }
};



postcss.config.js 파일 만들기

module.exports = {
  plugins: [
    // ...
    require("tailwindcss")("./src/tailwind.config.js"),
    require("autoprefixer")
    // ...
  ]
};

package.json 수정


"scripts": {
    "build:css": "postcss src/tailwind.css -o src/index.css",
    "watch:css": "postcss src/tailwind.css -o src/index.css",
    "start": "npm run watch:css & react-scripts start",
    "build": "npm run build:css react-scripts build",
    "test": "react-scripts test",
    "eject": "react-scripts eject",
  }

src/AppStyles.styles.tw.js  


import styled from "styled-components";
import tw from "tailwind.macro";

const AppStyles = styled.div.attrs({
  className: "w-full h-screen flex flex-col items-center justify-center"
})`
  & {
    h1 {
      ${tw`font-sans text-6xl font-hairline text-6xl text-teal-500`}
    }
    p {
      ${tw`text-gray-700 text-lg`}
    }
    h2 {
      ${tw`text-2xl font-hairline mt-5 text-teal-500`}
    }
    ul {
      ${tw`inline-flex`}
    }
    li {
      ${tw`mr-5`}
    }
    a {
      ${tw`text-blue-500 hover:text-gray-500 hover:underline`}
    }
  }
`;
export default AppStyles;


App.js
   

import React from "react";
import "./index.css";
import AppStyles from "./AppStyles.styles.tw";

const App = () => {
  return (
    <AppStyles>
      <h1>Greetings Earthling</h1>
      <p>
        Welcome to your Create-React-App / TailwindCSS / Styled Components
        template
      </p>
      <h2>Resources / Documentation</h2>
      <ul>
        <li>
          <a href="https://reactjs.org/docs/create-a-new-react-app.html">
            ReactJS
          </a>
        </li>
        <li>
          <a href="https://tailwindcss.com/">TailwindCSS</a>
        </li>
        <li>
          <a href="https://styled-components.com/">Styled Components</a>
        </li>
      </ul>
    </AppStyles>
  );
};

export default App;


  참고:  https://dev.to/dbshanks/an-efficient-react-tailwindcss-styled-components-workflow-458m
