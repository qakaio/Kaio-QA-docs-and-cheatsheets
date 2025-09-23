# Playwright JavaScript Cheat Sheet

A quick reference for the most important Playwright commands in JavaScript, with real usage examples.

```javascript
import { test, expect } from '@playwright/test';

test('Playwright Cheat Sheet Example', async ({ page }) => {

  // 1️⃣ Navigation
  await page.goto('https://example.com');
  await page.waitForLoadState('domcontentloaded');
  await page.reload();

  // 2️⃣ Interacting with input fields
  await page.fill('input[name="q"]', 'Playwright');
  await page.type('input[name="q"]', ' testing', { delay: 100 });
  await page.press('input[name="q"]', 'Enter');

  // 3️⃣ Clicking buttons and links
  await page.click('text=More information');
  await page.locator('button#submit').click();
  await page.getByRole('button', { name: 'Send' }).click();
  await page.locator('a#link').first().click({ force: true });

  // 4️⃣ Advanced selectors
  await page.locator('css=.my-class');
  await page.locator('xpath=//div[@id="main"]');
  await page.locator('text=Hello').nth(0);
  await page.locator('text=/hello/i');

  // 5️⃣ Waits
  await page.waitForSelector('text=Loaded');
  await page.locator('#my-element').waitFor({ state: 'visible' });
  await page.waitForTimeout(1000);

  // 6️⃣ Assertions
  await expect(page).toHaveURL(/example.com/);
  await expect(page.locator('h1')).toHaveText('Example Domain');
  await expect(page.locator('body')).toContainText('Example');
  await expect(page.locator('#element')).toBeVisible();

  // 7️⃣ Working with frames / iframes
  const frame = page.frameLocator('iframe#myFrame');
  await frame.locator('button#inside-frame').click();

  // 8️⃣ Working with dropdowns / selects
  await page.selectOption('select#options', 'value1');
  await page.selectOption('select#options', { label: 'Option 2' });

  // 9️⃣ Checkbox / radio
  await page.check('#checkbox');
  await page.uncheck('#checkbox');
  await page.locator('input[type="radio"][value="option1"]').check();

  // 🔟 Screenshots / PDF
  await page.screenshot({ path: 'screenshot.png', fullPage: true });
  // await page.pdf({ path: 'page.pdf' });

  // 1️⃣1️⃣ Cookies and storage
  const cookies = await page.context().cookies();
  await page.context().addCookies([{ name: 'token', value: '123', domain: 'example.com', path: '/' }]);
  await page.context().clearCookies();

  // 1️⃣2️⃣ Capturing text or attributes
  const text = await page.locator('h1').textContent();
  const attr = await page.locator('a#link').getAttribute('href');

  // 1️⃣3️⃣ Opening a new page / tab
  const newPage = await page.context().newPage();
  await newPage.goto('https://example.org');

  // 1️⃣4️⃣ Handling alerts / dialogs
  page.on('dialog', async dialog => {
    console.log(dialog.message());
    await dialog.accept();
  });

  // ✅ Complete example: Google search (mockable)
  // await page.goto('https://google.com');
  // await page.fill('input[name="q"]', 'Playwright');
  // await page.keyboard.press('Enter');
  // await page.locator('text=Playwright').first().click();

});
