使用ChromeDriver进行测试

项目主页地址https://sites.google.com/a/chromium.org/chromedriver/ ;
>webDriver 是一个在多个浏览器对webapp进行自动化测试的工具，他提供了打开页面，模拟用户输入，javaScript执行等等的功能。ChromeDriver是一个独立于Chromium的基于WebDriver协议的服务.ChromeDriver可以在android版本谷歌和桌面版本谷歌（Mac, Linux, Windows and ChromeOS）上运行;

Nw.js提供了一个基于NW.js的app的定制的ChromeDriver自动化测试工具;你可以通过[selenium](http://docs.seleniumhq.org/)这类的工具来使用它。
##开始

The following workflow uses [selenium-python](http://selenium-python.readthedocs.org/) to drive the tests. You can use any language port for Selenium to work with `chromedriver`.

### Installing

* Download ChromeDriver from NW.js website
* Extract the package and place `chromedriver` under the same dir that contains the NW.js binaries: `nw` for Linux, `nw.exe` for Windows, or `node-webkit.app` for Mac.
* Install `selenium-python` in your project:
```bash
pip install selenium
```

### Running

Suppose your app shows a form for searching from remote. The page basically something like this:
```html
<form action="http://mysearch.com/search" method="GET">
    <input type="text" name="q"><input type="submit" value="Submit">
</form>
```

Write a Python script to automatically fill in the search box and submit the form:
```python
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options
chrome_options = Options()
chrome_options.add_argument("nwapp=/path/to/your/app")

driver = webdriver.Chrome(executable_path='/path/to/nwjs/chromedriver', chrome_options=chrome_options)

time.sleep(5) # Wait 5s to see the web page
search_box = driver.find_element_by_name('q')
search_box.send_keys('ChromeDriver')
search_box.submit()
time.sleep(5) # Wait 5s to see the search result
driver.quit()
```

See http://selenium-python.readthedocs.org/ for detailed documents of `selenium-python`.
