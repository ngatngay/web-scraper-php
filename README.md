A simple PHP Web Scraper
================================

A screen scraping and web crawling library for PHP.

Requirements
------------

PHP 8.0+

Installation
------------

``` {.sourceCode .bash}
composer require ngatngay/php-web-scraper:dev-master
```

Usage
-----

``` {.sourceCode .php}
use Symfony\Component\BrowserKit\HttpBrowser;
use Symfony\Component\HttpClient\HttpClient;

$client = new HttpBrowser(HttpClient::create());
```

Make requests with the `request()` method:

``` {.sourceCode .php}
// Go to the symfony.com website
$crawler = $client->request('GET', 'https://www.symfony.com/blog/');
```

The method returns a `Crawler` object
(`Symfony\Component\DomCrawler\Crawler`).


Click on links:

``` {.sourceCode .php}
// Click on the "Security Advisories" link
$link = $crawler->selectLink('Security Advisories')->link();
$crawler = $client->click($link);
```

Extract data:

``` {.sourceCode .php}
// Get the latest post in this category and display the titles
$crawler->filter('h2 > a')->each(function ($node) {
    print $node->text()."\n";
});
```

Submit forms:

``` {.sourceCode .php}
$crawler = $client->request('GET', 'https://github.com/');
$crawler = $client->click($crawler->selectLink('Sign in')->link());
$form = $crawler->selectButton('Sign in')->form();
$crawler = $client->submit($form, ['login' => 'fabpot', 'password' => 'xxxxxx']);
$crawler->filter('.flash-error')->each(function ($node) {
    print $node->text()."\n";
});
```

More Information
----------------

Read the documentation of the
[BrowserKit](https://symfony.com/components/BrowserKit),
[DomCrawler](https://symfony.com/doc/current/components/dom_crawler.html),
[CssSelector](https://symfony.com/doc/current/components/css_selector.html)
and
[HttpClient](https://symfony.com/doc/current/components/http_client.html)
Symfony Components for more information.

License
-------

MIT license.
