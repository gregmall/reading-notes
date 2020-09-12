# Web Scraping with Javascript and NodeJS
* HTTP clients: querying the web
- **Request**
    - most widely used HTTP client in JS ecosystem
    - make an HTTP request with Request:
```
const request = require('request')
request('https://www.reddit.com/r/programming.json', function (
  error,
  response,
  body
) {
  console.error('error:', error)
  console.log('body:', body)
})
```
- **Axios**
    - promise based HTTP client that runs both in browser and NodeJS
    - straight forward
    - example:
```
const axios = require('axios')

axios
	.get('https://www.reddit.com/r/programming.json')
	.then((response) => {
		console.log(response)
	})
	.catch((error) => {
		console.error(error)
	});
```
    - example using async/await syntax:
```
async function getForum() {
	try {
		const response = await axios.get(
			'https://www.reddit.com/r/programming.json'
		)
		console.log(response)
	} catch (error) {
		console.error(error)
	}
}
```
- **Superagent**
    - has support for promises and async/await syntax
    - fairly straightforward
    - has more dependencies that Axios
    - example:
```
const superagent = require("superagent")
const forumURL = "https://www.reddit.com/r/programming.json"

// callbacks
superagent
	.get(forumURL)
	.end((error, response) => {
		console.log(response)
	})

// promises
superagent
	.get(forumURL)
	.then((response) => {
		console.log(response)
	})
	.catch((error) => {
		console.error(error)
	})

// promises with async/await
async function getForum() {
	try {
		const response = await superagent.get(forumURL)
		console.log(response)
	} catch (error) {
		console.error(error)
	}
}
```
* Regular Expressions: The hard way
- simplest way to web scrape without dependencies
- regular expressions aren't flexible 
- they get out of had for complex scraping
- example:
```
const htmlString = '<label>Username: John Doe</label>'
const result = htmlString.match(/<label>(.+)<\/label>/)

console.log(result[1], result[1].split(": ")[1])
// Username: John Doe, John Doe
```
* Cherio: Core JQuery for traversing the DOM
- allows you to use API of JQuery on the server-side
- example:
```
const cheerio = require('cheerio')
const $ = cheerio.load('<h2 class="title">Hello world</h2>')

$('h2.title').text('Hello there!')
$('h2').addClass('welcome')

$.html()
// <h2 class="title welcome">Hello there!</h2>
```
- does not work the same way that the web browser works therefore does not:
    - Render any of teh parsed or manipulated DOM elements
    - Apply CSS or load any external resource
    - Execute javascript
* JSDOM: The DOM for Node
- creates a DOM like object to be used in NodeJS
- makes it possible to interact with website or app you want to crawl, allowing for clicks on buttons and such.
- example:
```
const { JSDOM } = require('jsdom')
const { document } = new JSDOM(
	'<h2 class="title">Hello world</h2>'
).window
const heading = document.querySelector('.title')
heading.textContent = 'Hello there!'
heading.classList.add('welcome')

heading.innerHTML
// <h2 class="title welcome">Hello there!</h2>
```
* Puppeteer: The Headless browser
- allows you to manipulate the browsers programmatically just like a puppet would be manipulated by a puppeteer.
- provides a developer a high level API to control the headless version of Chrome by default
- can be configured to run non-headless
- Opens up possibilities not previously available:
    - you can get screenshots or generate PDFs of pages
    - You could crawl a Single Page Application and generate pre-rendered content
    - automate a lot of different user interactions like keyboard inputs, form submissions, navigation etc.
- can play a role in tasks outside scope of web crawling like UI testing, assist performance optimization, etc.
- example: 
```
const puppeteer = require('puppeteer')

async function getVisual() {
	try {
		const URL = 'https://www.reddit.com/r/programming/'
		const browser = await puppeteer.launch()
		const page = await browser.newPage()

		await page.goto(URL)
		await page.screenshot({ path: 'screenshot.png' })
		await page.pdf({ path: 'page.pdf' })

		await browser.close()
	} catch (error) {
		console.error(error)
	}
}

getVisual()
```
* Nightmare: An alternative to Puppeteer
- if you dislike puppeteer or are discouraged by the size of the chromium bundle then this is an ideal choice.
- example: 
```
const Nightmare = require('nightmare')
const nightmare = Nightmare()

nightmare
	.goto('https://www.google.com/')
	.type("input[title='Search']", 'ScrapingBee')
	.click("input[value='Google Search']")
	.wait('#rso > div:nth-child(1) > div > div > div.r > a')
	.evaluate(
		() =>
			document.querySelector(
				'#rso > div:nth-child(1) > div > div > div.r > a'
			).href
	)
	.end()
	.then((link) => {
		console.log('Scraping Bee Web Link': link)
	})
	.catch((error) => {
		console.error('Search failed:', error)
	})
```

# Document.querySelector()
* The Document method querySelector() returns the first Element within the document that matches the specified selector, or group of selectors. If no matches are found, null is returned.
* Syntax
```
element = document.querySelector(selectors);
```
- Parameters
    - selectors
        - A DOMString containing one or more selectors to match. This string must be a valid CSS selector string; if it isn't, a SYNTAX_ERR exception is thrown.
- Return value
    - An HTMLElement object representing the first element in the document that matches the specified set of CSS selectors, or null is returned if there are no matches.
- Exceptions
    - SYNTAX_ERR
        -  syntax of the specified selectors is invalid.

# Document.querySelectorAll()
* The Document method querySelectorAll() returns a static (not live) NodeList representing a list of the document's elements that match the specified group of selectors.
* Syntax
```
elementList = parentNode.querySelectorAll(selectors);
```
- Parameters
    - selectors
        - A DOMString containing one or more selectors to match against. This string must be a valid CSS selector string; if it's not, a SyntaxError exception is thrown.
- Return value
    - A non-live NodeList containing one Element object for each element that matches at least one of the specified selectors or an empty NodeList in case of no matches.
- Exceptions
    - SyntaxError
        - The syntax of the specified selectors string is not valid.

