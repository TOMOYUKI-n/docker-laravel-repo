## 利用方法

## Usage
1. click https://github.com/TOMOYUKI-n/docker-laravel-repo/generate
2. git clone & change directory
    ```
    $ git clone git@github.com:TOMOYUKI-n/docker-laravel-repo.git
    ```
3. execute command
    ```
    $ make create-project
    ```

## Structure
app container
    * Base image
        * php:8.1-fpm-bullseye
        * composer:2.1

web container
    * Base image
        * nginx:1.20-alpine
        * node:16-alpine

db container
    * Base image
        * mysql/mysql-server:8.0

### docker (lavavel)の場合
* Usage通り

## docker (lavavel + vue-cli)独立の場合
*  Usage + 以下の手順

1. create frontend dir
```
$ cd docker-template
$ vue create frontend
```
2. delete files
```
$ cd backend
$ rm -rf package.json webpack.mix.js
```
3. create vue.config.js
```
$ touch vue.config.js
```
```
module.exports = {
    outputDir: '../backend/public/app',
    publicPath: '/app',
    pages: {
        app: {
            entry: 'src/main.ts',
            template: 'templates/base.html',
            filename: `../../resources/views/spa/app.blade.php`,
        },
    },
}
```
4. make template dir
```
$ cd frontend
$ mv public/index.html templates/base.html
```
5. change web.php(in backend)
```
Route::get('/{any}', function () {
    return view('spa.app');
})->where('any', '.*');
```
6. add gitignore
```
$ cd backend
$ vi .gitignore
/public/app
/resources/views/spa
```
7. build
```
$ cd frontend
$ yarn build
```


## Reference
    * https://github.com/ucan-lab/docker-laravel
    * https://qiita.com/Okkun555/items/2b4f999fb310dfea933f
    * https://reffect.co.jp/vue/vue3-typescript#Vue3
