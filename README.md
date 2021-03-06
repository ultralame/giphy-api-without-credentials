giphy-api-without-credentials
===========

Simple to use Node.js module for the [giphy.com](http://giphy.com) API. All
search parameters and endpoints can be found on the [Giphy API documentation](https://github.com/giphy/GiphyAPI).

This version is a minor tweak of Austin Kelleher's [giphy-api](https://github.com/austinkelleher/giphy-api) module that simply sets `withCredentials` to `false` in the HTTP request.

Are you seeing this error in your browser app?

```
A wildcard '*' cannot be used in the 'Access-Control-Allow-Origin' header when the credentials flag is true.
```

If so, this right here is the module you're looking for.


![Giphy logo](http://giphy.com/static/img/giphy_logo_square_social.png)

## Installation
```bash
npm i giphy-api-without-credentials -S
```

## Importing
Since the original module receives the API key as an argument, you'll have to use `require()` instead of ES6 `import`
```javascript
// Require with custom API key
const giphy = require('giphy-api-without-credentials')('API KEY HERE');
// Require with the public beta key
const giphy = require('giphy-api-without-credentials')();
```

## [Phrase search](https://github.com/giphy/GiphyAPI#search-endpoint)
Search all Giphy GIFs for a word or phrase. Supported parameters:
- q - search query term or phrase
- limit - (optional) number of results to return, maximum 100. Default 25.
- offset - (optional) results offset, defaults to 0.
- rating - limit results to those rated (y,g, pg, pg-13 or r).
- fmt - (optional) return results in html or json format (useful for viewing responses as GIFs to debug/test)

```javascript
// Search with a plain string
giphy.search('pokemon', function(err, res) {
    // Res contains gif data!
});
```
```javascript
// Search with options
giphy.search({
    q: 'pokemon',
    rating: 'g'
}, function(err, res) {
    // Res contains gif data!
});
```

## [Giphy Id search](https://github.com/giphy/GiphyAPI#get-gif-by-id-endpoint)
Search all Giphy gifs for a single Id or an array of Id's

```javascript
//Search with a single Id
giphy.id('feqkVgjJpYtjy', function(err, res) {

});
```
```javascript
// Search with an array of Id's
giphy.id([
    'feqkVgjJpYtjy',
    '7rzbxdu0ZEXLy'
], function(err, res) {

});
```

## [Translate search](https://github.com/giphy/GiphyAPI#translate-endpoint)
Experimental search endpoint for gif dialects. Supported parameters:
- s - term or phrase to translate into a GIF
- rating - limit results to those rated (y,g, pg, pg-13 or r).
- fmt - (optional) return results in html or json format (useful for viewing responses as GIFs to debug/test)

```javascript
// Translate search with a plain string
giphy.translate('superman', function(err, res) {

});
```
```javascript
// Translate search with options
giphy.translate({
    s: 'superman',
    rating: 'g',
    fmt: 'html'
}, function(err, res) {

});
```

## [Random](https://github.com/giphy/GiphyAPI#random-endpoint)
Random gif(s) filtered by tag. Supported parameters:
- tag - the GIF tag to limit randomness by
- rating - limit results to those rated (y,g, pg, pg-13 or r).
- fmt - (optional) return results in html or json format (useful for viewing responses as GIFs to debug/test)

```javascript
// Random gif by tag
giphy.random('superman', function(err, res) {

});
```
```javascript
// Random gif with options
giphy.random({
    tag: 'superman',
    rating: 'g',
    fmt: 'json'
}, function(err, res) {

});
```

## [Trending](https://github.com/giphy/GiphyAPI#trending-gifs-endpoint)
Trending gifs on [The Hot 100](http://giphy.com/hot100) list
- limit (optional) limits the number of results returned. By default returns 25 results.
- rating - limit results to those rated (y,g, pg, pg-13 or r).
- fmt - (optional) return results in html or json format (useful for viewing responses as GIFs to debug/test)

```javascript
// Trending Hot 100 gifs
giphy.trending(function(err, res) {

});
```
```javascript
// Trending Hot 100 gifs with options
giphy.trending({
    limit: 2,
    rating: 'g',
    fmt: 'json'
}, function(err, res) {

});
```

## [Stickers](https://github.com/giphy/GiphyAPI#giphy-sticker-api)
[Animated stickers](https://giphy.com/stickers) are gifs with transparent backgrounds. All giphy-api functions
support stickers **except id**, which is not a supported Giphy sticker endpoint.
In order to use the sticker API instead of the gif API, simply pass the ```api```
property to a giphy-api function.
```javascript
giphy.search({
    api: 'stickers',
    q: 'funny'
}, function(err, res) {

});
```
