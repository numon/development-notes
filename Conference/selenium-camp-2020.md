## Selenium 4

link https://github.com/SeleniumHQ/selenium/projects/2

Task - 19, (
- config node, 
- support graphQL, 
- grid UI, 
- upgrade connection to http/2
- logsystem(datadog)
- migrate jar from selenium 3
- Use UNIX domain sockets for Docker communication
- rewrite location strategies use `by` not only `findByXXX`
)

No shadow DOM support 

in progress - 2  
PR - 119

## WebdriverIO
link - https://webdriver.io/docs/devtools-service.html
ability use  Chrome DevTools protocol "@wdio/devtools-service"
- Performance Testing (getMetrics, getDiagnostics, enablePerformanceAudits)
- Device Emulation
- Event Listener

#### React component 
```javascript
test('it should be displayed', () => {
    const myComponent = browser.react$('MyComponent')

    expect(myComponent.isDisplayed()).toBe(true) // pass
})
```

## Versioned Page Object

How to handle 12 version and localization ? Mixin ?
- https://github.com/Xotabu4/versioned-pageobjects

## OPS
- link aerokube - http://aerocube.com
- Working with Moon

## Espresso
- alex tiurin github/alex-tiurin