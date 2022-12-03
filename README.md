# Discuss - Fullstack Phoenix Application

## Step 01 - Creating Project, installing Tailwind, adding Inter font

### **Project creation**

`mix phx.new discuss --binary-id`

`cd discuss`

`mix ecto.create`

`mix phx.server`

### **Tailwind CSS installation**

Follow steps from: [Install Tailwind CSS with Phoenix](https://tailwindcss.com/docs/guides/phoenix)

### **Inter font installation**

1. Visit [Google Web Fonts Helper](https://google-webfonts-helper.herokuapp.com/fonts/inter?subsets=latin)

2. Select styles(regular(400), medium(500), semibold(600), bold(700))

3. Copy CSS; I chose Modern Browsers

4. Download files and unzip them

5. Inside vendor folder create fonts/inter folder. Move all .woff and .woff2 files in, and create inter.css file. Paste css we copied (step 3). Inside the inter.css file, make url paths look like this: ("inter-v12-latin-\*.woff2"). Basically, remove "../fonts/" from all urls

6. Inside discuss_web/templates/layout/root.html.heex add between **head** tags enter:

   `<link phx-track-static rel="stylesheet" href={Routes.static_path(@conn, "/assets/vendor/fonts/inter/inter.css")}/>`
   `<script defer phx-track-static type="text/javascript" src={Routes.static_path(@conn, "/assets/js/app.js")}></script>`

   Script tag already exist, and I just changed the path, so it doesn't console log the error later.

7. Inside config/config.exs find **config: esbuild** and replace **args** with:

   `~w(js/app.js --bundle --target=es2017 --outdir=../priv/static/assets vendor/fonts/inter/inter.css --bundle --loader:.woff2=file --loader:.woff=file --outdir=../priv/static/assets)`

8. Back in tailwind.config.js under the **let plugin = require("tailwindcss/plugin");** add:

   `const defaultTheme = require("tailwindcss/defaultTheme");`

   And replace **extend: {}** with:

   """

   extend: {
   fontFamily: {
   sans: ["Inter", ...defaultTheme.fontFamily.sans],
   },
   }

   """

9. Restart your app to see font styles applied:

   `mix phx.server`
