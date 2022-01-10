The Laravel docs on pagination seem to be incomplete. This repo shows the issue and suggests fixes.

## Installation

- Create a database called `paginate`.
- Migrate and seed the database
- Run `npm run watch`.

You will find the issue on the main page (`/`).

## The issue

The pagination component is rendered incorrectly. This is because Tailwind hasn't generated the required classes. With the default [Tailwind installation (for Laravel)](https://tailwindcss.com/docs/guides/laravel) it will search the `resources` folder but that's not where the pagination component is stored.

## Possible fixes

I found two possible fixes. I would add one of these to the docs.

- Add the vendor folder to the `content` array in `tailwind.config.js`.

```js
module.exports = {
  content: [
    "./resources/**/*.blade.php",
    "./resources/**/*.js",
    "./resources/**/*.vue",
    "./vendor/laravel/framework/src/Illuminate/Pagination/resources/views/*.blade.php",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

- Publish the views to the `resources` folder.

```
php artisan vendor:publish --tag=laravel-pagination
```
