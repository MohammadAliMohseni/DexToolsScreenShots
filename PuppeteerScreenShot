const puppeteer = require('puppeteer');

(async () => {
  const browser = await puppeteer.launch({ headless: true });  // Headless mode
  const page = await browser.newPage();
  
  // رفتن به لینک مشخص شده
  await page.goto('https://www.dextools.io/app/en/solana/pool-explorer');
  
  // تابع برای اسکرول کردن صفحه تا انتها و گرفتن اسکرین‌شات
  async function scrollAndScreenshot() {
    let previousHeight;
    try {
      while (true) {
        previousHeight = await page.evaluate('document.body.scrollHeight');
        await page.evaluate('window.scrollTo(0, document.body.scrollHeight)');
        await page.waitForFunction(`document.body.scrollHeight > ${previousHeight}`);
        await page.waitForTimeout(1000);  // تاخیر برای لود شدن محتوا
      }
    } catch (e) {
      // وقتی که صفحه دیگر اسکرول نمی‌شود
    }
    
    const timestamp = new Date().toISOString().replace(/[-:.]/g, '');
    await page.screenshot({ path: `screenshot_${timestamp}.png`, fullPage: true });
  }
  
  // اجرای تابع هر یک دقیقه
  setInterval(async () => {
    await scrollAndScreenshot();
  }, 60000);  // 60000 میلی‌ثانیه برابر با 1 دقیقه
  
  // اجرای ابتدایی تابع برای اولین بار
  await scrollAndScreenshot();
})();
