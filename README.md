# Testing Web-Applications with Selenium

In this assignment you learn how to build a maintainable test framework for testing web applications using JUnit and the [Selenium WebDriver][Selenium WebDriver]. 
Starting with a simple Selenium based test you will gradually improve the code to get a test system with abstraction layer, reusable functions and a separate test data pool.


## (1) Capture & Replay with Selenium IDE _(1 Point)_

In this exercise you learn the basics of automated web testing via capture and replay. We use [Selenium IDE][] for this.

### Prerequisites

- [x] A current version of either Firefox or Chrome web browser.
- [x] Selenium IDE browser add-on

### Instructions

1. Install Selenium IDE as extension to your browser (install either [Selenium IDE] for Firefox or Chrome).
1. Create a test case by using the 'record' function of Selenium IDE:
   1. Name the test case `BibSearchTest`
   1. Goto https://search-fho.obvsg.at/primo-explore/search?vid=FHO&search_scope=default_scope
   1. Use the search string `software testing` and click on the search icon
   1. Assert the number of entries returned by the search

1. Run the test and make sure it completes sucessfully.

1. :floppy_disk: Save the Selenium IDE project to [`src/side/BibSearchTest.side`](src/side/BibSearchTest.side).

Some hints:
* To start recording, click the red "rec" button at the very right of the IDE.
* Make sure to clean up the test cases after recording to get rid of unwanted commands that may have been recorded accidentially.

### Submission

When you're done...

- [x] push your changes to your upstream repository on GitHub.
- [x] on GitHub, [create a release][GitHub creating releases] with version `v1.0`.
- [x] upload the [link to your release][GitHub linking to releases] on the e-learning platform until the specified date and time before the next lecture.


## (2) JUnit Test using Selenium WebDriver _(2 Points)_

The goal of this exercise is to learn how to create a simple system test for a web application using JUnit and Selenium WebDriver. 

### Prerequisites

- [x] Completion of the previous part of the exercise (1)
- [x] Java and Maven (if you use an IDE like Eclipse or IntelliJ, that's **already included** :sunglasses:.)

### Instructions

1. This git repository contains a [Maven Project][] with example test cases

   The required libraries _Unit_, _Selenium WebDriver_ (and two more) are already set up as Maven dependencies
   Run the `mvn test` to make sure the setting is working correctly

1. Export the previsouly record `BibSearchTest` as starting point for your JUnit-based test case

   1. In SeleniumIDE, hoover over the name of the test case and click on the three dots appearing to the right. 
   1. Select `Export` > Java JUnit > Save as ... [`src/test/java/at/fhhagenberg/sqe/BibSearchTest.java`](src/test/java/at/fhhagenberg/sqe/BibSearchTest.java)

1. Adapt the exported test until it compiles and runs successfully

	1. Update the test to JUnit 5 (JUnit Jupiter)
	1. Replace the assertThat() with an assertEquals()
	1. Introduce waits to make sure the elements on the web page are shown before the are accessed 

### Submission
When you're done...

- [x] push your changes to your upstream repository on GitHub.
- [x] on GitHub, [create a release][GitHub creating releases] with version `v2.0`.
- [x] upload the [link to your release][GitHub linking to releases] on the e-learning platform until the specified date and time before the next lecture.


## (3) Page Objects _(3 Points)_

In this step you learn how to extend automated testing of (Web-based) GUIs to increase the maintainability and flexibility of your test implementation.

The test code written in the previous example has no abstractions and is therefore not well maintainable, especially when the page structure changes in a future version. Therefore, we want to create a more abstract domain-specific Test-API for the Widok web page to be able to write "high-level" tests that do not break on minor changes of the web page.

### Prerequisites

- [x] Completion of the previous part of the exercise (2)

### Instructions

Read the blog entry [Page Objects in Selenium][] about the use of the 'Page Objects' test pattern and refactor the test from the previous part into `BibSearchPageObjectsTest.java`.

The test cases should be independent from finding elements, clicks, key strokes, waits, etc. operating on specific elements of a Web page. These operations and specific elements should be moved to Page Object classes `SearchPage`, `ResultsPage`, etc. Put these classes into a separate package (e.g. `at.fhhagenberg.sqe.pageobjects`).

Note:
* Follow the examples provided at [Page Objects in Selenium] and [SeleniumHQ Wiki about PageObjects][SeleniumHQ Wiki PageObjects].
* Use the class `PageFactory` provided by Selenium to abbreviate the code in the Page Object classes. For further information see the aforementioned blog as well as the [Wiki documentation about PageFactories][SeleniumHQ Wiki PageFactory].
* Run your JUnit test cases – make sure they still pass.

### Submission

When you're done...

- [x] push your changes to your upstream repository on GitHub.
- [x] on GitHub, [create a release][GitHub creating releases] with version `v3.0`.
- [x] upload the [link to your release][GitHub linking to releases] on the e-learning platform until the specified date and time before the next lecture.


## (4) Data-driven Tests _(2 Points)_

The implemented test cases contain test code and test data. In this exercise you learn how to to increase the flexibility and maintainability of the tests by separating test data from test code.

### Prerequisites

- [x] Completion of the previous part of the exercise (3).

### Instructions

1. First, check https://junit.org/junit5/docs/current/user-guide/#writing-tests-parameterized-tests on details about JUnit’s support for parameterized test cases.

1. Create a parameterized JUnit `BibSearchParameterizedTest.java` test to repeat the following scenario
   1. Search for a term (e.g. 'software testing') and
   1. Check the number of found results

Please, extend your test case according to following instructions:
* Create a parameterized test that uses the page objects written in the previous step (3).
* Provide a list of search terms (e.g., "embedded software", "software quality", ...) and expected result numbers (e.g. "2.519", "9.795", ...) as parameter set; the parameterized test iterates over this parameter set.
* Use `CsvFileSource` to store the parameter values separately from the test code. Put the csv file in the folder `src/test/resources`.


### Submission

When you're done...

- [x] push your changes to your upstream repository on GitHub.
- [x] on GitHub, [create a release][GitHub creating releases] with version `v4.0`.
- [x] upload the [link to your release][GitHub linking to releases] on the e-learning platform until the specified date and time before the next lecture.

[GitHub creating releases]: https://help.github.com/articles/creating-releases/
[GitHub linking to releases]: https://help.github.com/articles/linking-to-releases/
[Selenium IDE]: https://www.seleniumhq.org/selenium-ide/
[Maven Project]: https://maven.apache.org/guides/getting-started/
[Page Objects in Selenium]: http://blog.activelylazy.co.uk/2011/07/09/page-objects-in-selenium-2-0/
[Selenium WebDriver]: https://www.selenium.dev/documentation/en/webdriver/
[Selenium Wiki PageObjects]: https://github.com/SeleniumHQ/selenium/wiki/PageObjects
[Selenium Wiki PageFactory]: https://github.com/SeleniumHQ/selenium/wiki/PageFactory
