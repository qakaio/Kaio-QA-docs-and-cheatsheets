
# 📱 Appium + WebdriverIO (JavaScript) Cheatsheet

## 🚀 Basic Setup
```bash
npm init -y
npm install @wdio/cli
npx wdio config
```
Run tests:
```bash
npx wdio run ./wdio.conf.js
```

---

## 🔍 Locating Elements
```js
const el = await $('~accessibilityId')      // By Accessibility ID
const el = await $('android=new UiSelector().text("Login")')  // By text (Android)
const el = await $('//android.widget.Button[@text="OK"]')     // By XPath
const el = await $('#elementId')            // By ID
```

---

## 🎯 Common Actions
```js
await el.click()                            // Tap on element
await el.doubleClick()                      // Double tap
await el.touchAction('tap')                 // Tap alternative
await el.setValue('text')                   // Type text
await el.addValue(' more text')             // Append text
await el.clearValue()                       // Clear text field
```

---

## 📜 Gestures
```js
await driver.touchPerform([                 // Custom gesture
  { action: 'press', options: { x: 200, y: 600 } },
  { action: 'moveTo', options: { x: 200, y: 100 } },
  { action: 'release' }
])

await driver.swipe(100, 600, 100, 100)      // Swipe (custom helper)
await driver.back()                         // Press back button
await driver.lock(3)                        // Lock device for 3s
await driver.unlock()                       // Unlock device
```

---

## 🧩 Assertions (expect-webdriverio)
```js
expect(await el.isDisplayed()).toBe(true)   // Check if visible
expect(await el.getText()).toContain('Login') // Text contains
expect(await el.getAttribute('enabled')).toBe('true')
```

---

## 🌐 Contexts & Switching
```js
const contexts = await driver.getContexts() // List all contexts
await driver.switchContext('WEBVIEW_1')     // Switch to webview
await driver.switchContext('NATIVE_APP')    // Back to native
```

---

## 🪄 Useful Helpers
```js
await driver.pause(2000)                    // Wait 2s
await driver.saveScreenshot('./screenshot.png') // Save screenshot
await driver.getDeviceTime()                // Get device time
await driver.getOrientation()               // Portrait / Landscape
await driver.setOrientation('LANDSCAPE')    // Rotate screen
```

---

## 🧱 Example Test
```js
describe('Login Test', () => {
  it('should login successfully', async () => {
    await $('~username').setValue('admin')
    await $('~password').setValue('123456')
    await $('~loginBtn').click()
    const successMsg = await $('~successMessage')
    await expect(successMsg).toBeDisplayed()
  })
})
```

---

## ⚙️ Tips
- Use `await` in all commands.
- Add implicit waits in `wdio.conf.js` (`waitforTimeout`).
- Use `beforeTest` hook to reset app state if needed.
- Combine WebdriverIO with Allure for reporting.

---

🧠 **Pro Tip:** Use Appium Inspector to easily find locators for your elements.
