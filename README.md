# tau_cucumber
Cucumber with JavaScript

chpater 1 BDD
	what it is
	importance
	value

chapter 2
Gherkin
	syntax 
		Given
		When
		Then
		But
		Background
		Features
		Scenarios
	Data Tables
	Best Practices

chapter 3 intro to cucumber
pros & cons of cucumber
right choice ?
Set up project

chapter 4: automation architecture with cucumber
	folder structure
	page object pattern
	connecting the layers

chapter 5: writing automated tests
	implement chapter 2
	dependency injection

chapter 6: visual validation 
 	Applitools w/ cucumber


BDD: behavior-driven development
	an example-based method for developing software.
many different collaborative activities and techniques performed by stakeholders
The Three Amigos
	the product owner 
	the tester 
	the developer 

 
Three Amigos meet to discuss and document 
	examples 
		how a system should act and be used. 
		describe
			how the software is intended to behave, 
			often illustrating a particular business rule or requirement.
	One of the major activities
Note that these examples 
	Outlines Only How a system or its features should behave.
	Not implemented 
The end result of discussing and documenting these examples:
		all parties should come to a mutual understanding of 
			how the feature will behave in various scenarios 
	and by extension 
			how the system itself should work.
note BDD 
	Not solely a testing technique
	a process of approaching your design
		forces you to think about the desired outcome before you code.
		like test-driven development (TDD)
Test cases and eventually automated tests 
	Should Be a byproduct of following a BDD approach 
and 
	having great properly structured examples.




BDD's value.
BDD major goals 
	narrow the communication gaps among team members 
	foster a better understanding of the customer's needs 
	promote continuous communication throughout software development process.
From the very beginning of developing software through to the end
	BDD involves the collaboration of All team members 
		to get an understanding of the needs of a system.
continuous collaboration few benefits:
	get the entire team speaking the same domain language 
	see silos broken down
	a shared understanding of what needs to be done. 
		extremely valuable especially in saving time and eventually money.
	the examples generated from team meetings 
		as executable artifacts that drive test automation
			i.e. develop our own examples and create automation from them.
new terms:
Three Amigos: the main stakeholders in the software development process: 
		product owner, tester, and developer.
Example-based: software development approach - leverages creation of examples to drive 
		discussion, understanding, development, and testing
An example: a description of How the software is intended to behave
		often illustrating a particular business rule or requirement.
Gherkin: a special syntax used when developing examples. 
		designed in a way for anyone to understand the behavior of a feature.






Gherkin is a special syntax that is used within BDD to document examples.
Gherkin uses a set of special keywords to give structure and meaning to executable specifications.
The files that are used to store Gherkin are referred to as feature files because each file is usually used to document the behavior for one feature
Each group of instructions that relate to the actions and behavior of an individual scenario of a feature is actually referred to as an example or a scenario
Some of the core keywords of Gherkin are: Feature, Scenario, Example, Given, When, and Then. We'll dive into what each keyword means, when to use them, and the best practices surrounding them.
This is the standard layout of an Example written in Gherkin — each line starts with a keyword followed by some descriptive text.

I've outlined here what each of the keywords is meant to achieve.
We start with the Feature keyword whose descriptive text outlines the feature, it's expected behavior, and how it relates to a business requirement.
Then we have a Scenario keyword whose descriptive text outlines the specific business situation related to the feature.
Following that we have Given, When, and Then — the cornerstone of Gherkin scenarios.

Each line in an example that begins with Given, When, or Then is called a Step.
These are responsible for explaining the state of a system or linking an action and the expected behavior. We’ll learn more about these keywords in a few slides.

Here is a scenario outlining the withdrawal feature of an ATM machine.
Feature: withdraw money. A customer should be able to withdraw cash from machine at any given time
Scenario: withdraw cash with money available
Given I have available funds in my account
When I select the withdraw option
Then I should get cash
Gherkin is written in English like statements making it easy for anyone to understand.

# This explains the feature and maps it back to an important business requirement. 

Feature: Withdraw money. A customer should be able to withdraw cash from the machine at any given time. 

# This is a title for the specific scenario of the feature. This outlines that the user is trying to withdraw money from their account when they have available money. 

Scenario: Withdraw cash with money available

# This outlines a precondition for the system. 

Given I have available funds in my account. 

# This is the action to be performed.

When I select the withdraw option

# This is the expected behavior of the system.

Then I should get cash. 

many more preconditions that need to be met, like money needs to be available in the ATM machine or the user has entered their pin correctly.
scenario should be linked directly to a business requirement of the system being built.

the Gherkin steps for the following scenario: Withdraw cash with no money available.
Feature: Withdraw money with No money available. A customer should be Not able to withdraw cash from the machine at a time when No money is available. 

Scenario: Withdraw cash with money Not available 

Given I do Not have available funds in my account. 

When I select the withdraw option

Then I should Not get Any cash

And Insufficient funds message Should Appear





Gherkin Syntax
keywords you can use and when to use them.
Given preconditions necessary for scenario to be executed by a user.
Given I am logged in as an administrator.
When describe the action to be performed. 
When I create a user.
Then describe the outcome from the action. 
Then the user is created.
And or But  these can be used to duplicate any previous keyword.
the scenarios below are identical and are both valid.
	Given I am logged in as administrator
	And 	I am a first time user
	When 	I create a user
	And 	I go to my profile
	Then 	I see my username

	Given I am logged in as administrator
	Given	I am a first time user
	When 	I create a user
	When 	I go to my profile
	Then 	I see my username

using And, and But can make a scenario easier to read.
Feature the first word in a Gherkin document or a feature file. 
The purpose: provide a high-level description of a feature
Scenario or Example a summary of the specific scenario of the feature of being described
Background used when you have a set of steps wanted repeated for multiple scenarios



Background gets executed Before each Scenario 
Background: 
Given I am logged in as administrator

Scenario: a user does Not see the getting started page 
Given I am Not a first time user
When I go to the dashboard
Then I do Not see a getting started page 

Scenario: a user Does See the getting started page 
Given I am a first time user
When I go to the dashboard
Then I do see a getting started page 

We have one Background followed by two Scenarios.
	this means Before the first step of each Scenario is executed, 
		the steps that belong to the Background will be executed. 
	both these Scenarios rely on a user being logged in as an administrator.
Scenario Outline 
useful when you want to run the same scenario with different values. 
used in conjunction with the Examples keyword
Examples referred to as data tables are used to outline the values to be used within a Scenario Outline. represented in a table format







	Scenario Outline: withdraw money
	Given I have <initial> dollars in my account
	When I withdraw <withdraw>
	Then I should have <remaining> dollars left

	Examples:
	| initial | withdraw | remaining |
	| 100    |    10         |     90          |
	|  20	|      5	      |	15	  |

We have one Scenario Outline and one Examples section with three rows.
In our Scenario Outline, we see some angled brackets (<variable>).
These brackets are on variables that will be replaced by the values in the data table.
The first row of the data table is the column headings, and these map to the variables that will be replaced in the Scenario Outline
The remaining rows contain the values to be used — each row represents a different scenario.
Below we have replaced the variable names in the scenario outline to translate what the first data row of the example would give us.

The combination of this Scenario Outline and data table would produce 2 scenarios with identical steps, just different values.

Gherkin best practices.
Create modular, reusable steps, and actually reuse them.
	create a step to withdraw any amount of money not just $100 
	common mistake: create Gherkin steps too detailed and not reusable.
Create behavior-driven steps, not procedural.
	Write steps as if being written by a user. 
	Avoid steps referring to specific elements or selectors. 
	This is a part of the process of Gherkin steps being developed by the 3 Amigos. 
		The step generated must be understood clearly by the stakeholders 
		and Not specific to some part of the code or an element on the interface.
Each Scenario should represent one behavior.
	limit the Scenario scope to 1 behavior for that feature.
Utilize Backgrounds and Scenario Outlines as much as possible.
	help to make your feature files more concise.
Avoid excessive use of And and But
If you find yourself using 3 or more And’s or But’s consecutively, 
			you aren't following the previous steps. 
	You may be trying to create 
		steps that are Not reusable 
  	or 
		steps that too tightly coupled with the UI.

Try Not to use punctuation (periods, commas) within step phrases.
	pain later on when trying to debug Why your steps aren't working.

Chapter 3 focusing on Cucumber.
We've done all this talking about BDD and Gherkin, 
what is Cucumber and how does it tie into all of this?
Cucumber is a tool that supports BDD and is used to execute Gherkin statements.
Cucumber works in a few steps
 reads each line of a Gherkin document
 validates that the statements conform to Gherkin syntax
 maps each Gherkin statement to some predefined logic. 
code that the automation engineer would have written
 executes that logic

This chapter and the remaining ones will be focused on 
	understanding Cucumber, 
	setting up a project that allows us to leverage Cucumber, 
	getting our hands dirty with creating our own Cucumber-based automation project.

BDD System requirements > Test Automation Project < > web browser
Gherkin Statements		Cucumber


Cucumber takes the already documented system requirements in the form of Gherkin,
 	does some processing with it which results in tests being automated 
		on various devices and environments.

Pros and Cons
1 benefit an extension from BDD: tests are understood by the entire team.
After following good BDD and Gherkin practices, 
	tests should be easily understood by each member of the project team.
2 Cucumber 
	allows for continued collaboration  
	increases the visibility among the entire team.
If tests are utilizing the same documentation that was created when the project was starting, 
	all members of the team can work together to ensure the current behavior and features are being tested.

3 Cucumber allows for a test to be refactored easily without changing the actual Gherkin statements.
	done by updating the underlying code.

the cons
1 with Cucumber you get extra layers of abstraction, 
	this can add time and effort to create and maintain a test automation project, 
	especially for team members Not familiar with Gherkin and Cucumber.
2 The use of Cucumber can lead to frustration. 
	If Not used with correct BDD and Gherkin and practices, 
		the resulting automation project will be harder to understand and maintain.
3 people tend to adopt tools over processes.
	if Cucumber is implemented as such without regard for the foundation provided by a BDD and sound Gherkin statements, the entire team can come to hate Cucumber and BDD as a whole and end up wasting money and resources trying to implement it as a standalone tool.





is BDD and Cucumber right for you?
a lot of benefits of BDD and Cucumber, 
it's Not always the best choice for a project or a team.
1 Don't use Cucumber only as an automation tool.
You will Not get the most value from it. 
2 Best used at the Beginning of a project
best to start out a project knowing the tool within processes you will be using. 
	You may face some friction from a team 
		if Cucumber is introduced halfway through a project, 
	especially if the team is unfamiliar with it.
	best to go into a project Knowing that you'll be using it 
	rather than decide halfway through 
		that you want to switch to a BDD approach.
3 have the resources to support it
	your team ready to take on a BDD approach to software development?
	have persons versed at BDD and Cucumber
	resources to train your team?
	          time to train your team?
	All of these questions are important to answer 
		before taking on BDD or any new process.
4 will your team actually benefit from BDD and Cucumber?
	Cucumber 
	may Not be as beneficial for 
		a very short project 
	or 
		a project with 2 or 3 people.
	may Not be very useful in a startup environment 
		where Not distinguished roles like 
			project manager, 
			developer, 
			or tester,
 		but rather these roles and responsibilities are melded together 
			with everyone being a little bit of each.
If after considering these with your team, 
	you believe you want to try out Cucumber and BDD, 
	then great !

Prerequisites for the rest of the course.
	Knowledge of the basics of JavaScript.
	Java, NodeJS and npm are mandatory for being able to run the test automation.
	https://www.oracle.com/downloads/
	https://www.oracle.com/java/technologies/javase-downloads.html
		select the LTS version
	
	https://nodejs.org/en/
	
	in terminal:
		java -version 
			java version "13" 2019-09-17
		node -v
			v14.17.3
		npm -v
			6.14.13
	Some prior knowledge of WebDriverIO.
		WebDriver tool allows us to interact with a browser and carry out actions as a user would.
			Knowing how to create and interpret regular expressions
			https://webdriver.io
		https://webdriver.io/docs/gettingstarted
	a text editor to actually create your test automation project.
		VSCode 
	



chapter 4 Automation Architecture with Cucumber.
						WebdriverIO \  
							       > Web browsers
						[Selenium]    /
BDD System requirements	Test Automation Project	     \/	
[Gherkin statements]	>	Cucumber        <	[	]


WebDriverIO: a tool that we use to automate the browser, 
	leveraging it to create our Cucumber project.
Within WebDriver is Selenium 
		Selenium what's actually responsible for carrying out actions on our browser. 
		Selenium relies on Java to work and is installed automatically when you install WebDriverIO.
In a project folder
	install WebDriverIO
		npm i webdriverio @wdio/cli

WebDriverIO does a great job of helping you set up your automation project, so you can focus on writing tests.

The cli command will ask you a series of questions that you need to answer, so WebDriverIO can bootstrap some files and install necessary dependencies to get you started.

To run the CLI, 
	run a file in the node modules folder

		./node_modules/.bin/wdio config

questions:						required answer:
	where test will be launched from 			local
	where our backend is locate				local
	framework						cucumber
	run WebdriverIO commands (sync or asynch)	sync
	feature files located					./features/**/*.feature
	step definitions located				./features/step-definitions
	reporter to use ?					spec (default) 	
		 https://www.npms.com/package/@wdio/spec-reporter
	add a service to test setup				 selenium-standalone
		https://www.npmjs.com/package/@wdio/selenium-standalone-service	 			base url?						http://google.com			
	




For services,
the selenium-standalone service  
	go down to the chromedriver, 
		deselect it by hitting [space] 
		select selenium-standalone. 
Selenium-standalone is what WebDriver will connect to access Selenium commands, 
and selecting this service allows it to be packaged within our project.

Two results of completing the cli are:
a WebDriverIO configuration file (wdio.conf.js) was created in the root of our project
the package JSON file (package.json) has some new modules

“@wdio/cucumber-framework”: “^5.11.12”
"@wdio/cucumber-framework": "^7.8.0",

	what allows WebDriverIO to understand Cucumber.
	This library communicates between 
		Cucumber and WebDriverIO 
		so WebDriverIO knows how to execute our tests.

						WebdriverIO \  
							       > Web browsers
						[Selenium]    /
BDD System requirements	Test Automation Project	     \/	
[Gherkin statements]	>	Cucumber        <	[ wdio/cucumber-framework]


WebDriverIO configuration file called wdio.conf.js, 
	see all the configurations we just selected with some really helpful comments.
go through the comments to understand what each property does, 
go through the API docs of WebDriverIO.
	https://webdriver.io/docs/api/

make a few changes to this configuration file.
 change the browser option here (in the Capabilities section) to Chrome, 
		so my test will run in Chrome 
		browserName: "chrome"
In the Test Configurations section change the log level to “warn”
 so I only see the warnings or errors in the console 
logLevel: "warn"
 in the Hooks section, uncomment the beforeSession function so I can load Babel.

the following code to require Babel 

add beforeSession: function(config, capabilities, specs) {
    require("@babel/register");
}

Babel is what will allow us to use some of the more modern features of Node and JavaScript.

https://babeljs.io
	a JavaScript compiler

All of these Hooks 
	seen in the wdio.conf.js file
	can be used to execute commands 
		before or after various events during your test. 
	come in very handy when you get to managing more complex test automation projects


						WebdriverIO \  
							       > Web browsers
						[Selenium]    /
BDD System requirements	Test Automation Project	     \/	
[Gherkin statements]	>	Cucumber        <	[ wdio/cucumber-framework]
			[Feature files]
			         /\
			         \/
			[Step Definitions]



Support Files are the third layer of our Cucumber automation.


						WebdriverIO \  
							       > Web browsers
						[Selenium]    /
BDD System requirements	Test Automation Project	     \/	
[Gherkin statements]	>	Cucumber        <	[ wdio/cucumber-framework]
			[Feature files]		/\
			         /\			 |	
			         \/			 |
			[Step Definitions]		 |
				/\		 |
			       [Support Files] <--------------|






put our general reusable functions - actions and assertions.
 Actions: actions want automation to do that will be executed in various Feature files.
 Assertions: functions that will perform actual verification of data 
			to judge if a test should pass or fail.
an effort to make our project robust and maintainable, 
		moving actions and assertions from the Step Definition files 
	and 
		to the Support Folder, 
	which will allow us to easily reuse them.


The last layer in our Cucumber automation, Page Objects.

						WebdriverIO \  
							       > Web browsers
						[Selenium]    /
BDD System requirements	Test Automation Project	     \/	
[Gherkin statements]	>	Cucumber        <	[ wdio/cucumber-framework]
			[Feature files]		/\
			         /\			 |	
			         \/			 |
			[Step Definitions]		 |
			  /\	/\		 |
		[Page Objects] <> [Support Files] <--------------|

Page Objects are a representation of a page in a website or application.
	contains selectors for elements on the page, 
and 
	methods responsible for interacting with the page. 
Basically, it allows us to separate the logic of our tests 
	from the static nature of our pages.
It's a very good way to have a maintainable automation project: 
	1 if some element on a page changes its selector, 
easily update the Page Object Without having to worry about modifying any test.
	2 if want to move away from Cucumber to a different framework, 
easily do so and still retain our Page Objects, 
only focus on changing our tests to match that new framework.
Preference: maintain the flow of logic; 
		have my Step Definition 
			call my Support files 
		   which calls my Page Object.
There will come a time where you may want 
	some logic to be handled outside of the Page Object. 
This approach allows you to keep a clean Page Object 
	by making the functions in there do actions that purely interact with the page.
An additional benefit is you can now build test workflows outside of your Page Objects and Step Definitions.
Putting most that complex logic in my Support file 
	helps me to maintain a modular Step Definition and Page Object file.
Great, you've completed our automation architecture.
Let's go through this diagram one last time.
When we start WebDriver IO, it searches for our tests which are our Feature Files
It then uses our Step Definitions to know how to execute each step. Based on how we code it, our Step Definition can either call our Page Object or Support File
Our Support File relies on data from our Page Object, whether that's an element or a method


