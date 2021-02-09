- It's just so simple. You just loop through page by page by changing url.

# NPM

```bash
npm init --yes
npm i --save request request-promise cheerio
```

# Code

```jsx
const request = require('request-promise')
const cheerio = require('cheerio')

//https://sfbay.craigslist.org/search/vol?s=0

async function scrape() {
    for(let index = 0; index < 360; index += 120) {
        const html = request.get('https://sfbay.craigslist.org/search/vol?s=' + index)
        const $ = await cheerio.load(html)
        $('.result-title').each((index, element) => {
            console.log($(element).text())
        })
        console.log("At page number " + index)
    }
}

scrape()
```