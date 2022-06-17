#### Puppeteer 
```shell
docker pull redsos/puppeteer:16-slim

# test
docker run -it --tz=Asia/Shanghai --network=host --hostname spider -v ${PWD}:/data/web -w /data/web --name spider redsos/puppeteer:16-slim node test.js
```

**test.js**
```javascript
const puppeteer = require('puppeteer');
const screenshot = 'example.png';

(async () => {
  const browser = await puppeteer.launch({
    executablePath: '/usr/bin/chromium',
    headless: true,
    appMode: true,
    devtools: true,
    args: [
      '--no-sandbox',
      '--disable-setuid-sandbox',
      '--disable-dev-shm-usage',
      '-–disable-gpu',
      '–-no-first-run',
      '–-no-zygote',
      '–-single-process'
    ]
  });

  const context = browser.defaultBrowserContext();

  await browser.defaultBrowserContext().overridePermissions('https://www.bing.com', ['clipboard-read', 'clipboard-write']);

  try {
    const page = await browser.newPage()
    await page.goto('https://www.bing.com/', { waitUntil: 'networkidle2' });
    try {
      await page.waitForFunction(
        text => document.querySelector('body').innerText.includes(text),
        {},
        "测试主题"
      );
    } catch (e) {
      console.log(`The text "测试主题" was not found on the page`);
      return;
    }
    await page.setViewport({
      width: 414,
      height: await page.evaluate(() => document.body.clientHeight),
    });

    await page.screenshot({ path: screenshot, fullPage: true });

  } catch (e) {
    console.error(e)
  } finally {
    browser.close()
  }
})()


```
