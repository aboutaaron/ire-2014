# When to scrape

## What is web scraping
The process of harvesting or collecting information from a web page

Automating server request

Can be done by writing a script (code) or with paid software tools, e.g., Helium Scraper
Can even be done simply by using Excel and wget

Considered the "gateway" to becoming a programmer (a lot of programmers go their start writing scrapers, including me!)

Involves many different technologies:

- HTTP
- HTML / CSS
- Web APIs
- Scripting languages (Python, Ruby, Perl)
- Spreadsheets and databases (CSV, SQLite, Excel)

## What can you scrape
- *Almost* any web page. If your browser can render the text, chances are you can scrape it.
  - That said, some pages use technologies like JavaScript and asp.net to render pages. Scrapers only see what's available when you click __View Source__ in the browser.

## Why Scrape
- AUTOMATION
  - download 80+ pdfs with a couple lines of code
  - Agency has data on webpage but won't release database through records request, e.g., California Sex Offenders Site

### Example with __Excel__ and __wget__
- First inspect the URL
```
http://www.meganslaw.ca.gov/cgi/prosoma.dll?zoomAction=Box&zoomAction=clickcenter&zoomAction=clickoffender&lastName=&firstName=&Address=&City=&zipcode=&searchDistance=.75&City2=&countyLocation=&zipcode2=&SelectCounty=FRESNO&ParkName=&searchDistance2=.75&City3=&zipcode3=&countyLocation3=&schoolName=&searchDistance3=.75&City4=&zipcode4=&countyLocation4=&refineID=&pan=&distacross=&centerlat=&centerlon=&starlat=&starlon=&startext=&x1=&y1=&x2=&y2=&mapwidth=525&mapheight=400&zoom=&searchBy=countylist&id=&docountycitylist=2&OFDTYPE=&W6=870100%0D%0A&lang=ENGLISH&W6=870100
```
Oooh, what's this? __&SelectCounty=ALAMEDA__

BINGO

- Create a list of California counties in Excel (http://oag.ca.gov/human-trafficking/sb1193/counties)
  1. Copy everying on this page
  2. Paste into Excel
  3. Find and replace to remove County from the County column
  4. Delete unused categories
  5. Uppercase county names and replace spaces with %20
![California Counties in a spreedsheet][1]

- Let Excel string functions be your friend
    1. Copy everything up until the county name (`http://www.meganslaw.ca.gov/cgi/prosoma.dll?zoomAction=Box&zoomAction=clickcenter&zoomAction=clickoffender&lastName=&firstName=&Address=&City=&zipcode=&searchDistance=.75&City2=&countyLocation=&zipcode2=&SelectCounty=`)
    2. Copy everything AFTER the county name (`&ParkName=&searchDistance2=.75&City3=&zipcode3=&countyLocation3=&schoolName=&searchDistance3=.75&City4=&zipcode4=&countyLocation4=&refineID=&pan=&distacross=&centerlat=&centerlon=&starlat=&starlon=&startext=&x1=&y1=&x2=&y2=&mapwidth=525&mapheight=400&zoom=&searchBy=countylist&id=&docountycitylist=2&OFDTYPE=&W6=870100%0D%0A&lang=ENGLISH&W6=870100`)
    3. Write a string function in D2 to combine the first column, the county column and the last column: `=B2&A2&C2`
    4. Copy down and ...
![Completed Spreadsheet][2]

- Now let's grab everything
 1. Copy everything in the URL column and paste it into a text file, e.g., urls.txt
 2. Install wget: see
 3. Now let's grab it all:
```
wget -mk -i urls.txt
```

- The Result

    
## Helpful things to pickup

- HTML and CSS

## Examples of scrapers for journalism

- http://projects.propublica.org/docdollars/
- http://cironline.org/reports/four-five-border-patrol-drug-busts-involve-us-citizens-records-show-4312
  - Scraped 3-to-4 years of press releases archives on the Border Patrol Website
  - Required crawling the website several times just retreieve every document (server issues, buggy website, etc.)

## Ethics
- robot.txt
- sleep functions
- Avoiding DDoS
- Avoid Passowrd-protected sites

## notes
Javascript pages
automation
useful modules
Don't rely on your scraper to last forever!

## Tools
- http://scrapy.org/
- http://palewi.re/posts/2008/06/15/terminal-recipe-how-to-download-an-entire-web-site-with-wget/
- http://ruby.bastardsbook.com/chapters/web-inspecting-traffic/


![enter image description here][3]


  [1]: https://s3-us-west-1.amazonaws.com/ire-2014/assets/spreedsheet1.png
  [2]: https://s3-us-west-1.amazonaws.com/ire-2014/assets/completed-spreadsheet.png
  [3]: https://s3-us-west-1.amazonaws.com/ire-2014/assets/wikipeda-viewsource.png "The document source of the Wikipedia page on web scraping"