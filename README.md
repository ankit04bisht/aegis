# aegis

(async () => {
  try {
    // Launch a new browser instance
    const browser = await puppeteer.launch();

    // Create a new page
    const page = await browser.newPage();

    // Navigate to Google Flights
    await page.goto('https://www.google.com/flights');

    // Wait for the page to load
    await page.waitForSelector('input[name="q"]');

    // Enter the origin and destination
    await page.type('input[name="q"]', 'New York');
    await page.type('input[name="d"]', 'Los Angeles');

    // Click on the search button
    await page.click('button[jsname="VXdfxd"]');

    // Wait for the search results to load
    await page.waitForSelector('.gws-flights-results__best-flights-heading');

    // Get the price result
    const priceElement = await page.$('.gws-flights-results__best-price');

    // Get the text content of the price result
    const priceText = await page.evaluate(element => element.textContent, priceElement);

    // Print the price result
    console.log('Price:', priceText);

    // Close the browser
    await browser.close();
  } catch (error) {
    console.error('An error occurred:', error);
  }
})();
