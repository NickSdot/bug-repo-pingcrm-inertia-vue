# Ping CRM fork to show port bug

This is a fork of the Inertia PingCRM demo. It serves to demonstrate a bug which leads routes to lose the port.

**Only edited files are:**
- package.json (installed BrowserSync)
- webpack.mix.js (setup for BrowserSync and stuff)

## Reproduce the issue

1. Navigate to https://pingcrm.test:3000/organizations.
2. Check the pagination links (correctly contains port) with mouse over.
3. Click on page two.
4. Check the pagination links again (**lost** the port).
5. Click on any pagination link, nothing will happen.
6. Open the console of your browser dev tools. You will see:

```
Access to XMLHttpRequest at 'https://pingcrm.test/organizations?page=3' from origin 'https://pingcrm.test:3000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.
```

```
xhr.js:177 GET https://pingcrm.test/organizations?page=3 net::ERR_FAILED
dispatchXhrRequest @ xhr.js:177
xhrAdapter @ xhr.js:13
dispatchRequest @ dispatchRequest.js:52
Promise.then (async)
request @ Axios.js:61
wrap @ bind.js:9
n.visit @ index.js:1
click @ index.js:1
invokeWithErrorHandling @ vue.esm.js:1865
invoker @ vue.esm.js:2190
original._wrapper @ vue.esm.js:7558
createError.js:16 Uncaught (in promise) Error: Network Error
    at createError (createError.js:16)
    at XMLHttpRequest.handleError (xhr.js:84)
```

## Installation

Clone the repo locally:

```sh
git clone https://github.com/inertiajs/pingcrm.git pingcrm
cd pingcrm
```

Install PHP dependencies:

```sh
composer install
```

Install NPM dependencies:

```sh
npm ci
```

Build assets:

```sh
npm run dev
```

Setup configuration:

```sh
cp .env.example .env
```

Generate application key:

```sh
php artisan key:generate
```

Create an SQLite database. You can also use another database (MySQL, Postgres), simply update your configuration accordingly.

```sh
touch database/database.sqlite
```

Run database migrations:

```sh
php artisan migrate
```

Run database seeder:

```sh
php artisan db:seed
```

Register Project on Machine

```sh
valet park pingcrm
```

Securing Project With TLS

```sh
valet park pingcrm
valet secure pingcrm
```

Run the dev server (the output will give the address):

```sh
npm run watch
```

You're ready to go! Visit Ping CRM in your browser, and login with:

- **Username:** johndoe@example.com
- **Password:** secret

## Running tests

To run the Ping CRM tests, run:

```
phpunit
```
