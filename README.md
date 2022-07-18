# LaravelSvelte
 laravel - laravel mix - svelte - tailwindcss - browser sync
 
 
##Steps that I followed
1. Create laravel project in current director
```
composer create-project laravel/laravel . --prefer-dist
```

2. Node Module
```
npm i
```

3. Install laravel mix
```
npm install wewowweb/laravel-mix-svelte
```

4. Now we need to configure webpack.mix.js 
https://laravel-mix.com/extensions/svelte
```
const mix = require('laravel-mix');
require('laravel-mix-svelte');
mix.js('resources/js/app.js', 'public/js')
    .sass('resources/sass/app.scss', 'public/css')
    .svelte({
        dev: true
    });
```

5 Open resources/js/app.js
```
import App from './components/App';
require('./bootstrap');
const app = new App({
    target: document.querySelector('#svelte-app')
});
```
Since we are targeting html with the id of svelte-app 
Let’s open welcome.blade.php file and add a div with svelte-app id
```
<div id="svelte-app"></div>
```

6. Create a file resources/js/components/App.svelte 
& add some test code

7. Open welcome.blade.php file and add this code before closing the body tag
```
<script type="text/javascript" src="{{ asset('js/app.js')}}"></script>
```

8. Install tailwind
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init
```

9. Open webpack.mix.js
```
mix.js("resources/js/app.js", "public/js")
  .postCss("resources/css/app.css", "public/css", [
    require("tailwindcss"),
  ]);
```

10. Configure tailwind.config.js
```
module.exports = {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

11. Open app.css
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

12. Add tailwind in html 
```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link href="{{ asset('css/app.css') }}" rel="stylesheet">
```

13. Run 
```
npm run watch
```

14. Run 
```
php artisan serve
```

15. Open webpack.mix.js then add the following line
```
mix.browserSync(
    {
        proxy: 'http://127.0.0.1:8000',
    }
)
```

16. Now 
```
run npm watch
```
The first time it will install couple of packages & then run the same command again

17. Done, You have laravel live reload now

