Azure Updates - Email Digest Logic App
======================

## Introduction / Context

Microsoft does a fantastic job of publishing content that allows their customers to track new features, events, etc. as they relate to Azure. That being said, In some cases it can be helpful to have a curated digest delivered to your inbox on a weekly basis!

This logic app was built to aggregate any number of RSS feeds in parallel, create a digest email and send it to the recipients of your choosing.  It can be easily customized to include additional feeds or static content.

## How the Logic App is Structured

![designer](images/designer.png "Logic App Flow")

This Logic App Runs on a recurrence trigger. By default it's set up to run every Monday at 7AM EST.

Upon execution Logic Apps kicks off 5 parallel flows. Each flow does the following:
- Connects to a given RSS feed and gets the latest articles
- Filters the articles to those that were published within the last week
- Initializes a variable to hold an HTML table
- Appends to the variable to open the HTML table
- If there are no articles, handles this condition and write a specific message to a single row in the table indicating this condition
- If there are articles, appends to the variable by writing a table row for each article
- Upon iterating through all articles, appends to the HTML table to close the article

When all of the content aggregation has completed, an email body is constructed and the email is sent out.

Notice the naming scheme of the steps. THis was done intentionally to maintain a specific order in the source JSON. When manipulated through the graphical designer, Logic Apps orders actions in alphabetical order. Having the parallel branches grouped in the source JSON makes it easier to parse and extend.

## Deployment

- Create a resource group
- Deploy the arm template using the CLI or PowerShell
- You'll need to provide email recipients as a parameter
- After deployment you will need to access the o365 connection in the portal and authorize it. Without conducting this step execution will fail.

Lorem