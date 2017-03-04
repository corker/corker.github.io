---
layout:     post
comments:   true
title:      "Three steps to click a button"
subtitle:   "How to keep UI automated tests clean"
date:       2017-03-04 12:00:00
author:     "Michael Borisov"
header-img: "img/post-bg-03.jpg"
---

I've been helping with test automation for a couple of projects. Every time we start fresh and have all good intentions
to keep our regression suite clean. Every time we end up tossing things around and spending time to adjust our scripts
in order to avoid big changes with every little new UI change. Is there an option to reduce the overhead? I know my specs
is a representation of original requirements. I also noticed that there is something usability engineers could benefit.

I've spent some time analyzing what levels of abstraction we have during automating specifications. I looked at what 
type of language we use on each of these levels and this is what I found:
1. A level of use cases. Where business processes and actors are defined;
2. A level of screens and scenarios. Where use cases translated into screens and scenarios;
3. A level of controls and actions. Where screens and scenarios translated into low level UI specific controls and actions.
 
Let's take a closer look on every level with some more or less practical examples. 
 
The level of use cases
---

I assume you know about behavior driven development, [Gherkin language](https://github.com/cucumber/cucumber/wiki/Gherkin)
and tools like [SpecFlow](http://specflow.org/). Using Gherkin language on this level makes a lot of sense. This level 
is very much about business meaning of our product thus it's good if business people can read this kind of tests. So, 
let our Gherkin scenarios speak the language Product Owner could understand and use as his own:     

{% highlight gherkin %}
Feature: Shopping
  Scenario: I want to buy a present for Christmas and I don't have any clue what to buy
    Given I know my budget
      And I know whom I buy a present
    When I ask for help to choose a present 
     And I tell about the person I buy a present 
     And I tell my budget 
    Then I'm offered with relevant options
{% endhighlight %}

I bet my Product Owner can read the scenario above and may be also find mistakes without any noticeable effort. I even
hope he could create scenarios for me so we could help each other and have a point for collaboration.

The level of screens and scenarios
---

At this level I'll refer to a [page object pattern](https://martinfowler.com/bliki/PageObject.html) explained by Martin 
Fowler. The page object pattern helps to separate low level clicks and objects from more meaningful screens and page 
blocks that actually makes our product do the stuff we build it for. These screens and blocks are specific to the 
product. Some teams even create a catalogue out of those blocks and reuse them through the product. These blocks usually
are tightly coupled with work that usability engineers are doing and this probably would be a topic for another article.
Still nothing like an input, button or label. To show an example I use [NOpenPage](https://github.com/corker/NOpenPage)
library. This is lightweight implementation for the page object pattern that extends [Selenium](https://github.com/SeleniumHQ/selenium).
The example shows SpecFlow steps:
 
{% highlight c# %}
[Binding]
public class MySteps
{
    [When(@"I ask for help to choose a present")]
    public void When_I_ask_for_help_to_choose_a_present()
    {
        Browser.Do(TheShopPage.Navigate);
        Browser.On<TheShopPage>().AskForHelpToChooseAPresent();
    }

    [Then(@"I'm offered with relevant options")]
    public void Then_Im_offered_with_relevant_options()
    {
        Browser.On<TheShopPage>().AssertRelevantOptionsOffered();
    }
}
{% endhighlight %}

This level need some effort from an person with development skills although the language could be clear for usability 
engineer as we speak about pages, blocks on those pages and scenarios that could be executed. Of course scenarios could 
be nested. Let's assume asking for help is something like a wizard. Then method AskForHelpToChooseAPresent could look
like this:

{% highlight c# %}
public class TheShopPage : Page
{
    public TheShopPage(IPageContext context) : base(context)
    {
    }

    public static void Navigate(IWebDriver driver)
    {
        driver.Navigate().GoToUrl("https://theshop.it");
    }

    public void AskForHelpToChooseAPresent(string gender, int age)
    {
        Control<Gender>().Choose(gender);
        Control<Age>().Choose(age);
    }

    public void AssertRelevantOptionsOffered()
    {
        Control<Offers>().AssertRelevantOptionsOffered();
    }
}
{% endhighlight %}

Level of controls and actions
---

So, now this should be clear. We went to the bottom. Buttons, labels and inputs live here. We put here all Selenium 
related code inside page objects implemented with NOpenPage:

{% highlight c# %}
public class Gender : PageControl
{
    public Gender(IPageControlContext context) : base(By.ClassName("gender"), context)
    {
    }

    public void Choose(string gender)
    {
        var input = Element.FindElement(By.Id(gender));
        input.Click();
    }
}
{% endhighlight %}

By following these three levels of abstraction:
+ I have clean specifications that business people and usability engineers can understand;
+ I can easily extend my specifications. Because I know on what level I need to introduce a change.  

Examples here are very abstract although I only want to show the idea of using business language on top, usability
language in the middle and keep technical low level details at the bottom. This approach helps a lot writing clean code 
for my automated tests.

Happy coding,<br/>
Michael Borisov.
