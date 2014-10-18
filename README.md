This project is now deprecated. The extensions library has been split into individual extensions:

* [Embed extension](https://github.com/concordion/concordion-embed-extension)
* [Exception translator extension](https://github.com/concordion/concordion-exception-translator-extension)
* [Logging tooltip extension](https://github.com/concordion/concordion-logging-tooltip-extension)
* [Screenshot extension](https://github.com/concordion/concordion-screenshot-extension)
* [Timestamp formatter extension](https://github.com/concordion/concordion-timestamp-formatter-extension)

with associated demo projects:

* [Exception translator extension demo](https://github.com/concordion/concordion-exception-translator-extension-demo)
* [Logging tooltip extension demo](https://github.com/concordion/concordion-logging-tooltip-extension-demo)
* [Screenshot extension demo](https://github.com/concordion/concordion-screenshot-extension-demo)


Introduction
------------------

This project demonstrates the usage of the Concordion [ExtensionsLibrary](http://concordion.org/ExtensionsLibrary.html) with [Selenium WebDriver](http://docs.seleniumhq.org/projects/webdriver/).

It contains an ExtensionsDemo index page that links to and runs the following tests:

- ScreenshotDemo demonstrates the [ScreenshotExtension](http://concordion.org/extensions/ScreenshotExtension.html).
- LoggingDemo demonstrates the [LoggingTooltipExtension](http://concordion.org/extensions/LoggingTooltipExtension.html).
- ExceptionTranslatorDemo demonstrates the [TranslatorExtension](http://concordion.org/extensions/TranslatorExtension.html).
    
Running the tests
---------------------------

The tests use Selenium's FirefoxDriver, so you'll need to have Firefox installed (or you could change the code to use a different driver).
    
The download includes support to run the tests with either <a href="http://www.gradle.org/">Gradle</a> or <a href="http://maven.apache.org/">Maven</a>.  
    
### Using Gradle
1. [Download](http://www.gradle.org/downloads.html) and [install](http://www.gradle.org/installation.html) Gradle (this has been tested with 1.0-milestone-3)
1. Unzip this package
1. From a command line opened at the location to which this package has been unzipped, run `gradle clean test`
1. View the Concordion output under the subfolder `build/reports/spec/org/concordion/ext/demo/selenium/`
    
### Using Maven
1. Download and install maven (this has been tested with 3.0.3)
1. Unzip this package
1. From a command line opened at the location to which this package has been unzipped, run `mvn test`
1. View the Concordion output under the subfolder `target/concordion/org/concordion/ext/demo/selenium/`

### Generating an Eclipse Project
If you use Eclipse and want to generate an Eclipse project:

1. [Download](http://www.gradle.org/downloads.html) and [install](http://www.gradle.org/installation.html) Gradle (this has been tested with 1.0-milestone-3)
1. Unzip this package
1. From a command line opened at the location to which this package has been unzipped, run `gradle cleanEclipse eclipse`
1. From Eclipse, the project can be imported from the `File` > `Import...` menu by selecting the import source `General` > `Existing Projects into Workspace`. Make sure the workspace is in a different folder than the project.
1. In Eclipse's Project Explorer, expand `src/test/java` > `org.concordion.ext.demo.selenium`, and run each of the tests `LoggingDemoTest` and `ScreenshotDemoTest` using `Run As` > `JUnit Test`.


What you should see
--------------------------------
The tests will open a Firefox browser and perform some Google searches.
    
### JUnit output
The tests should pass successfully, though the console output for the ScreenshotDemo and ExceptionTranslatorDemo tests will show failures and exceptions with the message:

> <-- Note: This test has been marked as EXPECTED_TO_FAIL

These tests deliberately contains failures in order to demonstrate features.  They use Concordion's `@ExpectedToFail` annotation to keep the JUnit passing (you'd normally only use this when you have a partially implemented feature).

### Concordion output
The output folder should contain the following 4 specifications.

#### ExtensionsDemo.html
This contains links to the following specifications.
    
#### ScreenshotDemo.html
This should show a failing example (red). Hovering the mouse over the failing example will show a screenshot taken when the failure occurred. Clicking on the failure will open the screenshot.

The screenshot extension is configured with a custom `SeleniumScreenshotTaker` class that uses Selenium's [TakesScreenshot](http://selenium.googlecode.com/svn/trunk/docs/api/java/org/openqa/selenium/TakesScreenshot.html) interface to take a screenshot of the web page.  The extension has a number of [configuration options](http://concordion.org/extensions/ScreenshotExtension.html#Configuration), for example to also take screenshots on successful examples and to set the image width.

It can also be used to [explicitly add screenshots](http://concordion.org/extensions/ScreenshotExtension.html#Explicit_screenshots) to the Concordion output.

#### LoggingDemo.html

This should show 2 blue information icons.  Hover over these icons to show information logged during the running of the example.

The bulk of the output is logged by the `SeleniumEventLogger` class, which implements [WebDriverEventListener](http://selenium.googlecode.com/svn/trunk/docs/api/java/org/openqa/selenium/support/events/WebDriverEventListener.html). 

The result text is logged from the `GoogleResultsPage`.

Logging the implementation details in this way allows us to ["retain a clear separation between intent and implementation, yet allow non-developers to be reassured that the test has been implemented correctly"](http://blog.davidpeterson.co.uk/2011/01/concordion-extensions.html).

By default this extension logs all output written using `java.util.logging`, with [configuration options](http://concordion.org/extensions/LoggingTooltipExtension.html#Configuration) to restrict the output that is included.
    
#### ExceptionTranslatorDemo.html
Shows the use of the TranslatorExtension to remove debug information from the WebDriver exception output.
    
Potential Issues
------------------------
### Proxy

If you are behind a HTTP proxy server, you may need to configure the proxy to allow access to www.google.com

The easiest way to do this may be to add the following lines to the Site() constructor:

>    System.setProperty("http.proxyHost", "<i>proxy.host</i>");
>    System.setProperty("http.proxyPort", "<i>proxy.port</i>");

where <i>`proxy.host`</i> is the host name of the proxy server, and <i>`proxy.port`</i> is the port number.

If your proxy requires authentication, you will also need to set the properties `http.ProxyUser` and `http.proxyPassword`.
  
Mailing List
-----------------
Feel free to discuss these examples on the Concordion [mailing list](http://tech.groups.yahoo.com/group/concordion).

See Also
-------------
The Extensions Library source code at https://github.com/concordion/concordion-extensions
