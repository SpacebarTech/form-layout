#### 8. Install all the packages

``` npm install ```

#### 9. Set up semantic release

``` semantic-release-cli setup ```

Follow prompt.\
Pick Travis CI\
Do not make a new travis.yml file\

#### 10. Setup main.js / main.vue file

Use either the main.js or main.vue file. Delete the other one.

#### 11. Build dist

``` npm run build ```

Make sure there are no errors

#### 12. Publish module

``` git add . ```\
``` git-cz ``` Follow the prompts\
``` git push origin master ```

#### 13. Update README.md

  1. Delete instructions
  2. use template below

[NAME OF MODULE]
========

[DESCRIPTION]

## Installation

  `npm install @spacebartech/[NAME OF MODULE]`

## Usage

## Tests

`npm test`
