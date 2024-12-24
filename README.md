const { Builder, By, until, Key } = require('selenium-webdriver');

(async () => {
    let driver = await new Builder().forBrowser('firefox').build();
    try {
        await driver.get('https://www.google.com');
        console.log((await driver.getTitle()) === 'Google' ? 'Test Case 1 Passed' : 'Test Case 1 Failed');

        await driver.findElement(By.name('q')).sendKeys('selenium', Key.RETURN);
        await driver.wait(until.titleContains('selenium'), 5000);
        console.log('Test Case 2 Passed');

        console.log((await driver.wait(until.elementsLocated(By.css('div.yuRUbf')), 100000)).length > 0 ? 'Test Case 3 Passed' : 'Test Case 3 Failed');
    } catch (e) {
        console.error(e);
    } finally {
        await driver.quit();
    }
})();
