### DON'T OVERLOOK THIS (needed for running tests) 
- have browsers you want to test on installed
- have browser webdrivers in $PATH for browsers you want to test

**WebDrivers:**
- Chrome:   https://sites.google.com/a/chromium.org/chromedriver/downloads
- Firefox:  https://github.com/mozilla/geckodriver/releases
- Safari:   in Terminal: safaridriver --enable
- Edge:     https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/
			
> Pay close attention to the version. Edge and Chrome WebDrivers' versions must be the same as Edge/Chrome browser that is installed.	
> For additional info: https://www.selenium.dev/downloads/

<br>
	
#### Using Selenium WebDriver 4 Javascript bindings:
> https://www.npmjs.com/package/selenium-webdriver
#### Selenium WebDriverJS bindings documentation:
> https://www.selenium.dev/selenium/docs/api/javascript/index.html

<br>

#### NEW PROJECT:
```
yarn init
yarn add jest @types/jest selenium-webdriver @types/selenium-webdriver typescript ts-jest
npx jest --init
```
> when asked if you want to use Typescript, choose NO <br>
> add-> `preset: "ts-jest",` <-to module.exports in jest.config.js

```
tsc --init
```
<br>
		
#### SETTING FROM THIS REPOSITORY (after cloning it):
```
yarn
```

> Just a note: might need 'yarn global add jest' if jest commands don't want to run tests.
> Might be windows/powershell issue but don't take my word for it.

<br>

#### HOW TO RUN TESTS
##### Required envs:
- WEBDRIVER 
	- determines on which WebDriver to run tests

##### Optional envs:
- LOCATION 
	- defaults to nothing, which runs tests locally
	- *remote* uses link in builder.ts, requires changing
- BINARIES 
	- defaults to nothing, which looks for default install location for used OS (ProgramFiles(and x86) for Windows or Applications for MacOS)
	- *custom* uses path in builder.ts, requires changing
- UI 
	- defaults to nothing, which runs WebDriver in GUI mode
	- *headless* runs browsers that have the capability (i.e. not Safari) in headless mode
	
> CHECK `package.json -> scripts` FOR MORE DETAILS:
	
##### Windows10 Powershell example: chrome, headless, default binaries, local
```
$env:WEBDRIVER="chrome"
$env:UI="headless"
jest partOfANameOfTest(s)(suites)
```
> MORE ON THIS: https://jestjs.io/docs/cli

<br>

##### MacOS zsh example: firefox, customBinaries, local
```
yarn test:customBinaries:firefox partOfANameOfTest(s)(suites)
```
> MORE ON THIS IN package.json

<br> **OR**

```
BINARIES=custom WEBDRIVER=firefox jest
```

<br>

Safari is special:
- can't headless
- always installed to default location
- haven't even tried to find remote runner so you'll have to add that case to builder.ts yourself
- WebDriver must not get out of focus so WebDrivers have to be run one by one

so for Safari it's:
```
yarn test:safari partOfANameOfTest(s)(suites)
```
<br> **OR** <br>
```
WEBDRIVER=safari jest --maxWorkers=1 partOfANameOfTest(s)(suites)
```
