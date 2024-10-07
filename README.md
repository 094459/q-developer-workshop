![Amazon Q Developer header](images/q-vscode-header.png)

## Next Generation Developer Tools

*A hands on guide to working with Amazon Q Developer. Made by DevRel with 💖.*

In this hands on lab, we are going to run through how to use the next generation of developer tooling to help make our jobs as developers more enjoyable and productive.

We will create a new application from scratch, and then build upon this and perform many of the tasks you would typically do as a developer. 

One thing to bear in mind before we start. Unlike other workshops, because of the non deterministic nature of these tools, there is no guarantee that the output will be the same as what your peers will see. What that means is that if you are working in groups, you can all expect different outputs. We have provided a [sample repo](https://github.com/094459/ada-python-demo-app) that you can use as a baseline, but we encourage you to explore and work with your own experiments - this is the most effective way of learning how these tools work.
 
The workshop is split into a number of different labs, with some lectures as well. This is what we will cover how we can use coding assistants like Amazon Q Developer to help us build applications quickly. We will look at some of the important features through labs, and help build your confidence in how you can use these yourself.

---

**What you will need**

You will need VScode IDE (or as an alternative, IntelliJ) with the following VSCode plugins installed

* Amazon Q Developer plugin - https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.amazon-q-vscode 
* Python plugin for VScode - https://marketplace.visualstudio.com/items?itemName=ms-python.python
* (optional) Database Client JDBC - https://marketplace.visualstudio.com/items?itemName=cweijan.dbclient-jdbc
* PostgreSQL cli tools - "brew install postgresql" (Mac) , use the windows installer to just install the cli tools (windows), or "sudo apt get install libpq-dev" (Ubuntu),"sudo dnf install libpq-devel" (Fedora)
* Python 3.10 or newer
* Postman (or similar tool) - we might need to interact with APIs that we create, so tools like Postman make this much easier
* git
* Docker or Finch - we will be spinning up local containers via a Docker Compose file, so you will need something like Docker or Finch to be able to run these. If you are not familiar with this, there are instructions on how you can run a local Postgres database using Docker or Finch in the Reference/Appendix section at the end of this workshop document.

**How do follow along**

Given the non deterministic nature of generative AI tools, the output you will get from running these prompts will be different to the output I got when creating this. You might be asking yourself, how will I know what is right or wrong, and how will I cope if things go horribly wrong? This is kind of intentional. Working with generative AI tools like Amazon Q Developer open you up to a new flow, a new way of working. If your expectation was that these tools will generate working code every time, then it is time to reset that expectation. The output that these tools provide will be your starting point, and get you 80% of the way there. You can then use Amazon Q Developer to help iterate and complete the remaining. If that does not work, at each different section of this lab, the git repo has a number of checkpoints. These have been implemented as branches, so you can start off without worrying if the previous lab failed.

Everyone running through this lab will have a different experience, but I hope the takeaway from this is a better understanding of the flow you will start to develop in using these tools to write software.

If you are working through this in a group setting, then the person running the lab will lead from the front and you can take your guidance from them.

# Setting up, and getting starting with Amazon Q Developer (20 min)

We are now ready for the first hands on part of this lab, setting up the generative AI developer tooling we are going to be using. We are going to be using Amazon Q Developer, a next generation developer tool that provides you with in-line code suggestions and a chat interface to help your developer flow. This is installed into your IDE (VSCode and IntelliJ are supported) via a plugin. Once the plugin is installed, we need to login using something that is called a Builder ID account. This allows you to access the Free Tier of Amazon Q Developer, without the need for an AWS account. So we first need to set that up, and then install the Amazon Q Developer plugin.

**Creating your Builder ID**

Creating a Builder ID is the first step in being able to use the Amazon Q Developer plugin. All you need is a valid email address to create a Builder ID. Head over to the [Builder ID page](https://profile.aws.amazon.com/) and then complete the creation by registering a valid email address. You can follow these screenshows to see the flow. After accessing the Builder ID page, you will need to provide an email address (1) and then create an alias (Your Name) (2). You will be sent an email verification which you will need to enter (3), and the email should only take a few moments to arrive (but check your SPAM folder just in case)(4)

![creation of a builder id flow](images/q-vscode-builderid-1.png)

Once you have received that code, enter it to validate your account (5), which should provide confirmation (6). You will be returned back to the initial screen, where you can now enter your email address (7) and password (8) and you should then see the Builder Profile page (9), where you can view your profile.

![completion of the builder id](images/q-vscode-builderid-2.png)

When you hear the term Builder ID when working with AWS services, this is the account they are referring to. It is separate from the AWS account, but is used by a number of services to provide access to those who want to try and AWS without the need for a full AWS account.


> **Logging out of your Builder ID** Sometimes you might need to log out of your Builder ID, and in order to do this you should head over to your [Builder ID Profile page](https://profile.aws.amazon.com/#/profile/details) and use the **Sign Out** button on the top left. Clicking on this will return you to the sign on page.


**Installing Amazon Q Developer**

Now that we have our Builder ID profile, lets install the Amazon Q Developer plugin. From the Extensions side bar, click on the icon to view the extensions marketplace. Search for "Amazon Q Developer" and you should be able to locate the Amazon Q Developer plugin (1). As of writing the latest version is v1.27.0. This is updated on a very regular basis, so make sure you either use the auto update, or check in regularly to take advantage of the improvements that are being made on a weekly basis.

![Installing the Amazon Q Developer plugin](images/q-vscode-install-1.png)

If the installation has been completed successfully, we will see a couple of things. First we will see a new Q icon on the left hand side bar (1), and you should also the the Amazon Q status bar at the bottom, with a X (2)

![Successfull installation of Amazon Q Developer](images/q-vscode-install-2.png)

If you click on that, you should see a menu pop up that shows that you are currently not signed in. We will do that next.

**Signing into Amazon Q Developer**

Now that we have our Builder ID created, and installed the Amazon Q Developer plugin, we can take the last step which is to login using that Builder ID. From the previous screenshot, if we click on the Q icon it will bring up the Amazon Q menu (3). When we click on that, we will see the login options for Amazon Q Developer (4) - there are two, we will ignore the "Use wit Pro Licence" and click on the "Use for Free" box and then click on Continue. This will bring up a pop up box (5). Take a note of the reference code, and then click on Proceed to Browser, which will bring up (6). Review that the code is the same as for the previous step, and then click on "Confirm and Continue", which will then bring up (7) to let you review the permissions that the Amazon Q Developer will need to work. If you are happy, click on "Allow Access" and if successfull, you will see the final screen (8) which you can close.

> **Note!** You might notice in the bottom left corner of VSCode the information panel that says that the Amazon Q plugin has opened up your web page. This will close automatically once the login has completed

![Signing into Amazon Q Developer using your Builder ID](images/q-vscode-signin-1.png)

Once you have logged in you will notice a few things. First the Q panel on the left hand side will be replaced with a chat window. You will also notice that at the bottom, the Amazon Q status bar will have changed form "X Amazon Q" to "|> Amazon Q". When you click on that, you will also see that you are now logged into Amazon Q using your AWS Builder ID.

![Sign in complete](images/q-vscode-signin-2.png)

We have now set up everything and are ready to go.

> **Logging out** If you want to log out, all you need to do is click on the Amazon Q status bar link to bring up the menu, and then select the Sign Out option. You can then repeat the process above to sign back in as you need

**Amazon Q Developer Settings**

Before we dive into the labs, it is worth going through how you can configure Amazon Q Developer and tailor it to your requirements. From the Extensions icon on the left icon bar, we can click on the cog wheel next to the Amazon Q Developer plugin, which will bring up the settings you can configure. This is handy to know incase you want to make changes later on. For the time being, we can leave this as is.

![Amazon Q Developer Settings](images/q-vscode-settings-1.png)

**Exploring Amazon Q Developer**

Like all developer tools, it is worth spending some time to explore and see how they work to really maximise the benefit to your productivity. In this section we will cover at a high level what Amazon Q Developer provides you with, but I would encourage you to explore.

*Amazon Q Developer menu options*

When we click on the Amazon Q status bar link at the bottom of VSCode, we will see the following pop up. This provides you will access to Amazon Q Developer options, most of which you will not need whilst you are using it, but you will come back to do certain things. Let's go through what each of these options provides.

![amazon q developer menu options](images/amazon-q-developer-plugin-menu.png)

* Pause Auto-Suggestions (Currently Running) - Amazon Q Developer provides you with suggested code blocks and snippets whilst working directly in your code. You can turn off this behaviour by clicking on this link (you will notice that it will then change to Resume Auto-Suggestions, Currently Paused, and the Amazon Q icon in the bottom status bar will also change). Every developer is different, and some prefer to have this option disabled, others enabled, so you will need to see what feels best for you. When paused, you can still invoke Amazon Q Developer to provide in-line code suggestions, by using the VSCode shortcuts (OPTION + C). Speaking of keyboard short cuts, lets check those out
* Open Code Reference Log - the underlying models that are used to power Amazon Q Developer use some open source code repositories, using Apache 2.0 and MIT licenced source files. Should code suggestions include portions from those projects, Amazon Q Developer will let you know by outputting this to the "Code Reference Log" which you can open by clicking on this menu option. When you click on this, you may see "Don't want suggestions that include code with references? Uncheck this option in Amazon Q: Settings". When using Builder ID you are not able to change this configuration, and the default option is to always include suggestions with code references. As you use Amazon Q Developer, check in here from time to time to see whether you are using code from those open source repositoires.
* Try inline suggestions Examples - this provides a quick tutorial to walk you through the basics of how to use Amazon Q Developer inline suggestions
* Run Project Scan - this kicks off a security scan of the code in the current project, using Amazon Q Developer and other AWS services to help you identify security issues before you ship the code. We will be exploring this later in the labs
* Open Chat Panel - this will open up the Amazon Q Developer chat panel if you close it
* Send Feedback / Connect with us on GitHub / View Documentation - these options provide you with additional ways you can provide feedback if Amazon Q Developer is not working the way you think it should
* Open Settings - will open the Amazon Q Developer plugin settings options (as covered above)
* Sign Out (Connected as AWS Builder ID) - allows you to log out of your current session, with the identity displayed. During this lab, it will always be AWS Builder ID. 

*Keyboard shortcuts*

You can control how you invoke Amazon Q Developer via the various key shortcuts, including customising these to how you work.

![keyboard shortcuts for Amazon Q Developer](images/amazon-q-vscode-shortcuts.png)

One of the key short cuts to know when you are working in the inline editor, is the < and > arrows. These allow you to cycle through suggestions when you are prompted by Amazon Q Developer.

*Chat Interface*

You can open the Chat Panel by clicking on the Amazon Q status bar link at the bottom, which by default, will make it appear on the left hand side with the other application artifacts (like files open, git files, etc). You can drag the Chat Panel to the right hand side, as in the screenshot below, which I find helpful as it allows me to see my files in the project, the files I am editing, and then also provide me with my chat interface.

![Amazon Q Developer Chat interface](images/q-vscode-screen-layout.png)

You can click on the + to open several chat sessions. When using Amazon Q Developer, the plugin will remember the conversations and use that in subsequent responses. This is very helpful when using Amazon Q to work through and troubleshoot issues. We will see this throughout this lab. You can open up to ten of these different tabs or conversations.

Amazon Q Developer also has some power features which are invoked using the /

* /dev invokes the Amazon Q Developer Agent for software development, and with this, it can create files, add new features, add tests, create documentation, and more. This is one of the most powerful features of Amazon Q Developer, as it will start to take your prompt, break it down into tasks, and then start working through the different tasks in realtime. It explores the files in your workspace to understand your project, and it will share which files it has reviewed and used, files it might want to change, and any new files it has created. Once finished, you will be able to review, check, and if desired, accept these updates.
* /transform invokes the Amazon Q Developer Agent for transformation that helps you migrate Java 8 projects to Java 17, taking the effort out of modernising your applications. We will not be using that during this lab, but it is worth knowing about if you are working with old Java applications.

**Note!** When using /dev and /transform with Builder IDs, you have limited quota. You can find out more on the official [Amazon Q Developer pricing page](https://aws.amazon.com/q/developer/pricing/), if you scroll half way down you will see a table which outlines the limits you have open to you.

*Menu bar integration*

When you are working on our code within the editor, Amazon Q Developer provides a handy way to quickly invoke it to perform a number of functions. When working on a file, you can select a portion of code, or even if you want the whole thing, and then when you RIGHT CLICK, you will see an "Send to Amazon Q" menu option, which when you select you will see a number of options:

![Amazon Q Developer editor menus](images/q-vscode-editor-menu.png)

* Explain - this will send whatever you have highlighted to the Amazon Q Chat panel, and ask Amazon Q to help explain what this code does
* Refactor - this will review the snippet and suggest ways you can improve code readability or efficiency, among other improvements
* Fix - this is handy if you are seeing linting errors in your code, or are trying to resolve other issues with your code
* Optimise - this will look to see if it can optimise the performance of the code you have selected
* Send to Prompt - this will copy the portion you have selected and then move it to the Amazon Q Developer Chat Panel. You can then provide your own prompt to ask Amazon Q Developer what you want it to do. This is an easier way than copy/pasting the code snippet yourself.


*Context*

During the lecture you will have heard about large language model context sizes. In effect, this is the amount of information that can be provided to tools like Amazon Q Developer, for them to then reason and make suggestions. When working with Amazon Q Developer, there are two modalities you need to be aware about.

* When using the Amazon Q Developer inline code - when you are in the editor, latency and performance are critical, and so this affects the context size that Amazon Q Developer is able to use. It will take the prompt provided, as well as additional information within the file its working on 
* When using the Amazon Q Developer chat interface - when you use the Amazon Q Developer chat, you will notice there is a small number just below the submit icon (4000/4000). This is the size of the context window. From a latency perspective, there is less need to be very responsive, and so this allows Amazon Q Developer to provide a bigger context size.
* Amazon Q Developer chat inteface tabs - you can open up several chat interface tabs by clicking on the + next to the Chat. Each of these will be new conversations with new context. You can open up to ten of these chat conversations.

Amazon Q Developer also uses things such as open tabs in VSCode, as well as key files depending on programming language (for example, the pom.xml in Java) to add additional information to help it make better suggestions.

If you want to get low level and see this working, you can check the logging of the Amazon Q Developer plugin and see this in action.

*Indexing your local workspace*

Amazon Q Developer allows you to index your local workspace which can then be used as part of the context when using the Chat interface. This is a very powerful feature that allows you to bring in additional information to help steer the direction of the output from Amazon Q Developer. For example, maybe you have some existing coding standards you want to influence any code that is generated by Amazon Q. Another way that you can use this is to help personalise the kind of output that Amazon Q Developer generates. You will see some examples of this in the .qdeveloper folder. There are two files, once called "java-expert.md" and the other "opensource.md". These contain additional prompts that will shape the output. A common way you can use this is to create shorter output, perhaps just outputing the code rather than any explaination.

You use this feature from within the Amazon Q Developer Chat interface. You invoke it with @ which will then display the available options. Currently this is only @workspace.

To use @workspace however, you need to first set this up. From the Amazon Q Developer plugin settings, you will see some new options.

![Amazon Q Developer plugin configuration options to enable workplace indexing](images/q-workspace-settings.png)

Once enabled you will need to restart VSCode. When you restart it, from the OUTPUT tab, there will new option - Amazon Q Language Server. The first time VSCode starts it will explore the current workspace and start to index files.


![Amazon Q Developer workplace indexing logs](images/q-workspace-index.png)

!*Note!* This feature is still in preview, so there may be some rough edges. One thing I have found is that occasionally you might need to delete the indexes and then restart VSCode to kick of the re-index process.

One the indexing has completed, @worksplace will be ready to go.


*Amazon Q Developer logs*

You can access the various Amazon Q Developer plugin logs from the OUTPUT menu option that appears when you have the terminal section in VSCode. When you select the pull down menu, you will see Amazon Q and Amazon Q Logs. The latter provides detailed information about how the plugin is working and interacting with the backend generative AI services powered by Amazon Bedrock.

*Additional learning resources*

I have just covered the basics here, but we are always plublishing new content that shows how other developers are doing cool things with Amazon Q Developer. If you want to know more, head over to [community.aws](https://community.aws/amazon-q)

**Understanding how to ask Amazon Q Developer questions**

As you explore the world of generative AI developer tools, one thing you will need to think about is that in order to get useful output and results, you need to ensure that you provide tools like Amazon Q Developer, the right input. What do I mean?

The "Prompt" or "Chat Interface" is how tools like Amazon Q Developer know what they need to do, in the same way that when you are using a search engine, you enter terms you want to search for. It is tempting to treat these chat interfacts like search, but that will lead to poor results. Here are some things to think about that will improve the output from tools like Amazon Q Developer.

* Provide as much information as possible - rather than say "Add a README" as a prompt, a better one would be "Create a README.md file for this project that will explain what this project does, what the key files are, and how to run it."
* If the output is not what you expect, you can use follow up prompts to help steer and improve the output. Using terms like "Can you provide a more detailed response" or "Can you give a code example" are good ways you can maintain the context and memory of what has been asked before, and refine the output
* If the ouput is good, use the thumbs up and down to provide feedback - this will ensure that the responses improve over time
* If the output is bad, use the thumbs down and use the additional link to provide feedback - this will help ensure that you do not get the same poor results back
* Rephrase the question - sometimes, the  output you get will not be great. This is part of the nature of how these tools work. Sometimes, it is better to reword or re-think your prompt and try again
* Remember these tools are non deterministic - it is easy to forget that every time you run the same prompt, you are likely to get different results and output. That is the nature of these tools - it is a feature not a bug
* Debug errors by copying important parts of error messages - one of the powerful ways these tools can help you improve your productivity is by reducing context switching and allowing you to stay within your code editor whilst troubleshooting and fixing errors. Just grab the most peritent part of the error, and then send it to the Amazon Q Developer Chat panel and ask questions like "How do I resolve this error", or "What does this mean". 

Ok, you are now up to speed with the Amazon Q Developer plugin, and it is time to see what you can achieve with it.

## Building our new application

In this lab we are going to build an application in Python that will allow us to get feedback by creating polls, and then letting people vote. We have chosen Python as it makes it easy to follow along and understand how these next generation developer tools work. The application will initially have some basic functionality, an MLP - Minimum Lovable Product.We will be using Amazon Q Developer to help us add code and improve the basic functionality.

**Lab 01-0 Checking our setup**

Make sure that you have installed the Amazon Q Developer plugin before proceeding.

Throughout this hands on workshop we will be using a GitHub repo that has multiple branches that we can switch to in order to validate the work we have done, and also make sure we always have a starting point that works.

From a terminal, navigate to a new directory where we will start work (I am using projects here as this is what I use, but feel free to switch this to whatever you use), and then type in the following to clone the repo into your workspace. 

```
cd ~/projects
git clone https://github.com/094459/q-workshop-app.git
cd q-workshop-app
```
Fom the terminal, we can now start VSCode by typing in "code ."

Once VSCode has started, the first thing we need to do is make sure that we are running in the Python virtual environment we created. Open up a Terminal in VSCode, and from that terminal run the following commands:

```
python -m venv .venv
source .venv/bin/activate
```

You should notice that the Terminal inside VSCode now has the (.venv) prefix, indicating you are running in this new virtual Python environment.


You can explore the files that we checked out by using the tree command (if you have this installed) we can see that we have our starting files which we will build from here.
```
├── LICENSE
└── docker
    ├── postgres.yaml
    └── start.sh
```

You might wonder why we need these files. When we build our application we are going to be using a database. To keep things simple and local, we will start a local Postgres database. We have made this easy by providing a Docker file that will allow you to get this up and running. 

From VSCode Terminal, use the + to open up another Terminal. You can now start a local Postgres database running in a Container by running the following commands (change docker for finch if you are using that)

```
cd docker
docker compose -p local-postgres -f postgres.yaml up
```

That should download the container image and then start. When it finishes it should look something like this

```
...
psql-1 |2024-10-03 10:56:54.704 UTC [1] LOG:  starting PostgreSQL 15.6 (Debian 15.6-1.pgdg120+2) on aarch64-unknown-linux-gnu, compiled by gcc (Debian 12.2.0-14) 12.2.0, 64-bit
psql-1 |2024-10-03 10:56:54.705 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
psql-1 |2024-10-03 10:56:54.705 UTC [1] LOG:  listening on IPv6 address "::", port 5432
psql-1 |2024-10-03 10:56:54.709 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
```

If you have psql running on your machine, you can try logging into the local Postgres database. Otherwise you can use the VSCode plugin Database Client JDBC which allows you to do this from VSCode and has a nice GUI interface for connecting to and running queries.

We are now ready to start.


**Lab 01-1 Our application - Creating our Data Model**

The application we want to build is a simple tool for collecting feedback - the humble Poll. We are going to start by using Amazon Q Developer to help us define the data model for this application, providing various prompts that will help provide a good starting point of what we want our data model to look like. Once we have our data model, we can then start to create some code artefacts.

Our data Model is a reflection of the User requirements of our application. For this simple Poll, we might use the following to describe this.*Create a data model for a simple Voting application. Users will log in using an email addresses. Users will be able to create new Polls, or update/delete existing Polls. Users can create multiple Polls. Polls can have between 2 and 5 options. Once Polls are created, the End Users will be able to vote on a Poll. We will capture the source IP address of End Users when voting.*

**Task 1**

We will now see what Amazon Q Developers thinks when we ask it. Open up the Amazon Q Developer Chat interface, and from the prompt enter the following:

> Create a data model for a simple Voting application. Users will log in using an email addresses. Users will be able to create new Polls, or update/delete existing Polls. Users can create multiple Polls. Polls can have between 2 and 5 options.Once Polls are created, the End Users will be able to vote on a Poll. We will capture the source IP address of End Users when voting.

Give the non deterministic nature of these tools, it is hard to predict the output you will get. What does the output look like? When I ran this, this is the output Amazon Q Developer provided:

```
Certainly! I'll create a data model for a simple Voting application based on your requirements. I'll use Python classes to represent the data model, which can be easily adapted to various database systems or ORMs (Object-Relational Mappers) like SQLAlchemy or Django ORM. [1]

Here's a data model that fulfills your requirements:

from datetime import datetime
from typing import List

class User:
    def __init__(self, id: int, email: str, password_hash: str):
        self.id = id
        self.email = email
        self.password_hash = password_hash
        self.polls: List[Poll] = []

class Poll:
        self.id = id
        self.title = title
        self.creator = creator
        self.created_at = created_at
        self.options: List[PollOption] = []
        self.votes: List[Vote] = []

    def add_option(self, option_text: str):
        if len(self.options) < 5:
            new_option = PollOption(id=len(self.options) + 1, text=option_text, poll=self)
            self.options.append(new_option)
        else:
            raise ValueError("A poll can have a maximum of 5 options")

class PollOption:
    def __init__(self, id: int, text: str, poll: Poll):
        self.id = id
        self.text = text
        self.poll = poll

class Vote:
    def __init__(self, id: int, poll: Poll, option: PollOption, ip_address: str, voted_at: datetime):
        self.id = id
        self.poll = poll
        self.option = option
        self.ip_address = ip_address
        self.voted_at = voted_at

```

We are going to now try again, and this time use a feature of the Amazon Q Developer that will help us personalize the output that we get. In the project directory you git cloned, you will notice there is a folder called ".qdeveloper" which contains a single file - DBA.md - Open the file and review it. 

We are going to use this file to help tailor the output of Amazon Q Developer, using the @workspace feature. This feature is disabled by default (it is currently a BETA feature) and so we are going to have to enable it. Once enabled, this is going to index your local VSCode workspace, looking at all the files including the DBA.md. Once the indexing has completed, we can use the @workspace in the Amazon Q Developer chat interface to add specific files as part of the context. In this case we are using it to help steer the kind of output we want Amazon Q Developer to give us, but we can use it for lots of other use cases too.

Right, lets enable this now.

**Task 2**

Open up the Amazon Q Developer plugin settings (remember from the overview, using the link at the bottom of VSCode to bring up the menu, where you will find the "Open Settings" option).

Look for the "Amazon Q: Workspace Index" section. This will have a check box next to it that will be blank (not set). Click on the box to enable this and then close the settings tab.

From the Terminal menu options, select OUTPUT and then from the pull down menu, click on the down arrow to bring up all the different output otions. You should have a NEW entry called "Amazon Q Language Server". Click on this and you should see that it has started to index the files in this project. It will look something like this:

```
LSP server starts
Loaded model from /Users/ricsue/.vscode/extensions/amazonwebservices.amazon-q-vscode-1.27.0/resources/qserver
[Warn  - 16:44:27] Unknown tokenizer class "CodeSageTokenizer", attempting to construct from base class.
Using number of intra-op threads: 2
Embedding provider initialized.
Validating embedding:s1 0.26636229613723583, s2 0.20119692089068866, s3 0.4491747579475595
Indexing 10 files under rootpath: /Users/ricsue/Projects/amazon-q/workshop/q-workshop
Starting index 10 files
Indexing done for 1/10 files
Indexing done for 2/10 files
Indexing done for 3/10 files
Indexing done for 4/10 files
Indexing done for 5/10 files
Indexing done for 6/10 files
Indexing done for 7/10 files
Indexing done for 8/10 files
Indexing done for 9/10 files
Index complete! Take 21.269275083s. Total 10 files, 133 chunks
Index saved to /Users/ricsue/.aws/amazonq/cache/cache/d7118a0df04a8a3a08dcf3d3f868d272db1601d953802875b4be8bda158fe919-0.9-VSCode.index
```
You can also see the logs by changing the OUTPUT menu option to "Amazon Q Logs"

```
2024-10-03 16:44:27.504 [info] LspController: Starting to build vector index of project
2024-10-03 16:44:27.717 [info] LspController: Found 10 files in current project /Users/ricsue/Projects/amazon-q/workshop/q-workshop
2024-10-03 16:45:31.223 [info] AB Testing Cohort Assignments []
2024-10-03 16:45:36.759 [info] LspController: LSP server CPU 0.03829787234042553%, LSP server Memory 413.34375MB
```

>*Tip!* The directory where these indexes are created can be deleted if needed. As this is still a BETA capability, sometimes you might need to delete the index files and then restart the IDE to recreate them if you start getting strange error messages. 

We can now try this feature out.

**Task 3**

From the Amazon Q Developer Chat interface, type @ and you should see workspace appear. Tab to complete that, and then add the following to your prompt:

> @workspace DBA Create a data model for a simple Voting application. Users will log in using an email addresses. Users will be able to create new Polls, or update/delete existing Polls. Users can create multiple Polls. Once Polls are created, the End Users will be able to vote on a Poll. We will capture the source IP address of End Users when voting.

Hit return and review the output. You should get very different output this time. This is what mine looks like.

```
CREATE TABLE users (
user_id SERIAL PRIMARY KEY,
email VARCHAR(255) UNIQUE NOT NULL,
password_hash VARCHAR(255) NOT NULL
);

CREATE TABLE polls (
poll_id SERIAL PRIMARY KEY,
user_id INTEGER REFERENCES users(user_id),
title VARCHAR(255) NOT NULL,
created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE poll_options (
option_id SERIAL PRIMARY KEY,
poll_id INTEGER REFERENCES polls(poll_id),
option_text VARCHAR(255) NOT NULL
);

CREATE TABLE votes (
vote_id SERIAL PRIMARY KEY,
poll_id INTEGER REFERENCES polls(poll_id),
option_id INTEGER REFERENCES poll_options(option_id),
ip_address INET NOT NULL,
voted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```

As you can see, this time we have got SQL code rather than Python code. What just happened? Well, the @workspace used the local DBA.md file as input (context) to help shape the output. You can experiment with this if you want. For example, I added the following line -> - My preferred database is PostgreSQL so provide any SQL that works with PostgreSQL.

Create a folder called "data" and create a new file called "voting-app.sql", and paste the SQL into this file. We will use this file to create the tables in our Postgres database.

*Getting Amazon Q Developer to help explain code*

Amazon Q Developer is integrated into the VSCode IDE which allows you to easily invoke it to help you with certain activities. For example, from the IDE open up the voting-app.sql we have just created and select all (CTRL + A). Right click on the menu and select "Amazon Q" and from the list of options, select "Explain".

In the Amazon Q Developer Chat interface, you should see a good explaination of the SQL and how it works. You can use this feature any time you have code that you might want a quick summary of how it works.

*Creating our local database*

The next thing we want to do is get our application data model up and running in the local Postgres database. From the Terminal in VSCode, run the following command:

```
psql -h 127.0.0.1 -p 5432 -U postgres -f data/voting-app.sql
```

After asking for the password (which should be change-me unless you changed the Dockerfile), you will see the following output:

```
Password for user postgres: 
CREATE DATABASE
psql (14.12 (Homebrew), server 15.6 (Debian 15.6-1.pgdg120+2))
You are now connected to database "voting" as user "postgres".
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE TABLE
CREATE FUNCTION
CREATE TRIGGER
```

Congratulations, you have created your data model, and we can now start to build the application code.

**Complete:** When your database now has your created tables and indexes, you can proceed to the next lab.

---

**Lab 01-2 Building the application - APIs**

Now that we have defined the data model for our application, we can start to write some code. We are going to use Amazon Q Developer Agent for software development to automate the creation of this code. Amazon Q Developer Agent for software development takes your prompt and then breaks this down into a series of tasks. As it starts to reason about those tasks, it will start to review the existing files you have in your project (in this case, our sql code) and then start writing code. Once Amazon Q has finished, it will present the final output for review, allowing you to test and review the code. At this point you can then provide feedback to adjust or accept the code as is.

**Task 4**

Open up the Amazon Q Developer Chat interface, and from the prompt enter hit the / key, and from the pop up select /dev and hit enter. You should now copy the prompt below and then hit enter again.

> Using the voting-app.sql for reference, create a Python web application using the Flask framework that will create a Voting application. The application will allow users to register and then login. Once logged in, users will be able to create Polls. The application will also provide a URI that will allow people accessing the application to vote on a specific Poll.

This process is likely to take 4-5 minutes, but keep an eye on what is happening as the status of tasks will be updating in realtime, as well as it displaying what files it is using and what files it will be creating.

Once it has completed, click on the files in the "Code Suggestions" box. When I ran this prompt, it only generated a single file (app.py). Review the code, and if you are happy, use the feedback icon (Thumb UP or Thumb DOWN) to provide feedback before hitting the "Insert Code" button.

You now have a starter application. The next step is to see if this will run.

**Task 5**

We can use Amazon Q Developer to help us understand how to run this application. From the Amazon Q Developer Chat interface, etner the following prompt:

> @workspace How do I run this application

Review your output. Is it helpful and accurate? This is what I got when I ran this.

```
First, ensure you have all the necessary dependencies installed. This application requires Flask, Flask-SQLAlchemy, and psycopg2 (for PostgreSQL connection). You can install these using pip:

pip install Flask Flask-SQLAlchemy psycopg2-binary


Update the database URI in the app.py file if necessary. The current configuration is

app.config['SQLALCHEMY_DATABASE_URI'] = 'postgresql://username:password@localhost/voting'

Now you're ready to run the application. In the directory containing app.py, run:

python app.py

```

It was pretty accurate actually, and after making the suggested updated and trying to start the app via Python.

```
python app.py

 * Serving Flask app 'app'
 * Debug mode: on
WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
Press CTRL+C to quit
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: 514-261-686

```

Job done. We have our application up and running.

**Task 6**

The code generated by Amazon Q Developer will vary given the non deterministic nature of the tool. To keep things simple, I have provided the output of my prompt in the branch "lab-02" which you can access by running the following command:

```
git checkout lab-02
Switched to branch 'lab-02'
```

And you will see the code. You might notice that the application provides only the APIs, so I will need to use a tool like Postman to interact with the application. Alternatively you can use Curl to send data to the application. Try the following commands:

```
curl -X POST http://127.0.0.1:5000/login \
     -H "Content-Type: application/json" \
     -d '{"email": "ricsue@amazon.co.uk", "password": "change-me"}'
```

Which should generate the following error

```
{
  "message": "Invalid email or password"
}
```

Because we have not created our user account. We can use the /register endpoint to do that using the following command:

```
curl -X POST http://127.0.0.1:5000/register \
     -H "Content-Type: application/json" \
     -d '{"email": "ricsue@amazon.co.uk", "password": "change-me"}'
```

Which will output

```
{
  "message": "User registered successfully"
}
```

We can now try logging in again, and this time you should be successfull.


```
curl -X POST http://127.0.0.1:5000/login \
     -H "Content-Type: application/json" \
     -d '{"email": "ricsue@amazon.co.uk", "password": "change-me"}'


{
  "message": "Logged in successfully"
}
```


> **Hint!** If you did not generate any working code, or are stuck, then you can get on the same page by switching to the following branch before proceeding with the next lab.
> 
> ```
> git checkout lab-02
>
> ```
> This should switch you to a version of the code that works and will set you up for the following lab.


Congratulations, you have created a running application that provides APIs that model your application functionality.

**Complete:** When you have got your application up and running, you can proceed to the next lab.

---

**Lab 01-3 Building the application**

In the previous lab the prompt guided Amazon Q Developer to create API's and provide a robust backend which we can work on. What if you just wanted a quick working prototype? Well we can adjust the prompt and ask /dev to create a fully working application. In the next two tasks we are going to first of all retry this and create a fully working prototype, and then after this, go back to our API and see if we can get Amazon Q Developer to help complete the application so we can use it with a web browser.

**Task 7**

In the Amazon Q Developer Chat interface, I used /dev and pressed enter and then pasted the following prompt:

> Using the voting-app.sql for reference, create a Python Flask Voting web application. The home page will allow users to register and then login. Once logged in, users will be able view existing Polls, to create new Polls. The application will also provide a URI that will allow people accessing the application to vote on a specific Poll.

This time you will notice that it also generates the web application components. Some things to look out for:

* I did notice that somes the code will reference supporting files but will not create the html pages. If this happens with you, make sure you provide further feedback and then add in your prompt "You have not generated the html resources for the code can you create those as well"
* At least a few times the code looked good, but the Models had incorrect names or values. This is easily fixed - review the code and adjust any issues with names that you see

It is likely that the code will not work first time, so we are going to use Amazon Q Developer to help us troubleshoot any issues we see. These are some of the prompts I used to help me fix small issues with the code:

>@workspace I have updated the app.py, including renaming the Models. Can you review and tell me how to update the html resources in templates
>
>@workspace the code is generating this error when creating Polls - TypeError: 'poll' is an invalid keyword argument for Option
>
>@workspace with the current code, when looking at My Polls, clicking on any links generates a 404
>
>@workspace add a new route that displays the results of a poll
>

You will notice that I am using @workspace so that it looks at the code as reference (context) for providing me suggestions.


As you adjust your code, run the application and test it. You should this time be able to use a standard web browser to access the application. Make sure that you test 1/ registering a new user and logging in, 2/ creating a new poll, 3/ voting and viewing the results

I played around and generated two versions of this fully functioning application.If you want to review this code that I created, then use the following commands:

```
 git checkout lab-03
```
or
```
 git checkout lab-02a
```

Explore the code and then run it in the same way as before.


**Task 8**

Before proceeding, take a few seconds to clear the local Postgres of any data that you might have added as part of the previous tasks. I find the VSCode plugin [Database Client JDBC](https://marketplace.visualstudio.com/items?itemName=cweijan.dbclient-jdbc) makes this super easy. Alternatively connect to the local Postgres database and run the following commands:

```
DELETE FROM "votes";
DELETE FROM "poll_options";
DELETE FROM "polls";
DELETE FROM "users";
```

We are going to go back to our Voting API application, and use Amazon Q to help us build new functionality that will allow us to use it from a web browser. Lets switch to that branch

```
git checkout lab-02
```

We are going to stop/start the Amazon Q Workspace indexing (go to Amazon Q Developer plugin settings, uncheck the box and then after a second or so, re-select it). Now from the Amazon Q Developer Chat interface, enter the following prompt, remembering first to hit the @ key and then press enter for workspace:

> @workspace looking at the Voting application in app.py, update the code so that I can access and use this via web browser. Include any html pages I need to create.

Take time to review the output and then implement it. Once you have done that, try running the application. Register a user, login, create a Poll and then try voiting. It is likely that you will see errors. I have captured the state of the code recommended to me in the [following branch](https://github.com/094459/q-workshop-app/tree/lab-04) which you can check for yourself. In this example, I could do everything but when trying to view a poll it would error.

* A couple of the routes are missing the return statement
* There is an issue with an undefined value called new_vote

Use the Amazon Q Developer menu integration to highlight code segments and then use the "Fix" and "Send to Prompt" to see if you can resolve the issue. You will find the working code in [this branch](https://github.com/094459/q-workshop-app/tree/lab-04a)


Will be using this version of the application going forward.


---


**Lab 01-4 Running a Security Scan**

We have some code, but how robust is it? In this lab we are going to use a feature of Amazon Q Developer to scan the project and help us shift left with security. This allows us to proactively detect and then resolve issues in our code, closing that feedback loop. Lets see how this works.

**Task 9**

We will start from a working version of our code.

```
git checkout lab-04a
```

Click on the Amazon Q on the bottom status bar to bring up the Amazon Q Developer options, and select "Run Project Scan" from the menu. You should see that this kicks off and a popup will appear in the bottom right of your VSCode.

![Clicking on Amazon Q Developer and starting a security scan](images/q-vscode-security-scan.png)

This will take a minute or two, but it should come back when its finished and tell you that it has found an issue. If you click on the issue that is in the Terminal editor area, you will be taken to the issue in your code. 

![Amazon Q Developer found an issue](images/q-vscode-finding.png)

If you hover over the highlighted code in VSCode, a pop up will appear which will provide more information. Sometimes, like in this case, you will be offered a Quick Fix, but other times you will need to use the View Problem link and let Amazon Q Developer help you with the issue. In this case, we have the Quick Fix, so lets see what it does.

![Amazon Q Developer quick fix](images/q-vscode-finding-details.png)

When we click on the link we are provided with a couple of options. If you select the EXPLAIN option, you should see the Amazon Q Developer Chat interface start to provide more info on how to resolve this issue.

![Amazon Q Developer explaining how to address the issue](images/q-vscode-finding-options.png)

It suggests I make modifications to the code - here is what is recommends:

```
# Construct the database URI using environment variables
db_user = os.environ.get('DB_USER', 'postgres')
db_password = os.environ.get('DB_PASSWORD')
db_host = os.environ.get('DB_HOST', '127.0.0.1')
db_name = os.environ.get('DB_NAME', 'voting')

if not db_password:
    raise ValueError("Database password not set in environment variables")

app.config['SQLALCHEMY_DATABASE_URI'] = f'postgresql://{db_user}:{db_password}@{db_host}/{db_name}'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['SECRET_KEY'] = os.urandom(24)
```

Once I make these changes and then save the file, I kick off another Security Scan. This time it comes back with no findings.

![No security issues found ](images/q-vscode-no-security-findings.png)

I now try and run the application again. Before I do this, I set an environment variable for the password. Restarting the application shows that everything is working, and I now have a working application that is passed the first level of security checks.

---

**Lab 01-5 In code suggestions**

In the previous lab we were able to get our working application through its first security scan. In this lab we are going to explore the in-line coding assistant feature of Amazon Q Developer. This feature allows you to prompt whilst you are editing code, and then choose from a number of options that Amazon Q Developer will provide. When you install the Amazon Q Developer plugin, this is enabled and running by default. You can check the status by clicking on the Amazon Q on the bottom status bar. The very first line will say "Pause Auto-Suggestions Currently Running" which is letting you know this feature is enabled and waiting. If you want to stop this, click on the option, and it should switch to "Resume Auto-Suggestions Currently Paused" and you will notice that the icon on the bottom of the status bar next to Amazon Q has changed. Make sure that this is ENABLED for this section.

> **Tip!** You might prefer to invoke the in-inline suggestions manually via key short cuts. If you prefer, then disable the auto suggestions and then use the keyboard short cut as and when you want Amazon Q Developer to provide guidance from a prompt.

**Task 10**

To try this out we are going to add a new feature to our application - an about page that explains how to use this application. To make sure everyone is on the same page, use the following code to get to the same starting code:

```
git checkout lab-05
```


Open up the app.py file. We are first going to create a new function that will return a random quote which we will include in our About page. Just above the #Routes section add the following and hit return. Watch carefully what happens in the editor.

> Yoda Wisdom - create a function that will return a single, random quote of wisdom from Master Yoda

![Initial prompt](images/q-vscode-yoda-function-prompt.png)

It should start to bring up some light grey code. Amazon Q Developer will review this prompt and then suggest some code. Sometimes the first thing it will suggest is not what you want, so you can use the Left and Right arrows on the keyboard to cycle between options.

![Initial code for Yoda function](images/q-vscode-yoda-function-start.png)

Sometimes when Amazon Q provides the initial code, you might still need to complete it. In this instance, it has provided me with some examples, and I now need to either close the array, or add some additional items.

![Completing the code suggestion](images/q-vscode-yoda-function-complete.png)

In this instance I am going to close the array. When I hit return, Amazon Q Developer continues to provide code suggestions to complete the function.

![Finished function](images/q-vscode-yoda-function-end.png)


Now that we have our function, we can use this when adding a new About page. We will try a new prompt from the editor, this time moving the editor to the #Routes section, and after the initial root route.

> Add a route for /about that will display a new html page called about.html that includes a quote from the get_yoda_wisdom function

![initial prompt for the about page](images/q-vscode-about-prompt.png)

When we are happy with what Amazon Q Developer has suggested, we hit return to complete the code.

![completed new route for about](images/q-vscode-about-finish.png)

We are not quite there yet, as we have the function, and a new route defined but we do not have the html page. This time we are going to ask the Amazon Q Developer Chat interface to provide the code. From the chat interface we provide the following prompt:

> Create code for a new about.html that uses the /about route and displays some text that shows how this application works. It should also display the output from the yoda function that is passed into this html

Feel free to experiment with different prompts to see what you get.

If you want to see the completed code when I ran these prompts, you can check out the branch [here](https://github.com/094459/q-workshop-app/tree/lab-05)


---

**Lab 01-6 Fixing our code**

**Task 11**

As you are working on your code, you are occasionally going to encounter issues which take time to debug, and then fix. Amazon Q Developer can help decrease the time it takes to find those issues and suggest fixes. In this lab we are going to explore some of those options.

We are going to checkout a branch of the application that has issues/problems which we need to fix. Run the following commands

```
git checkout lab-05-broken
```

Try running the application and then accessing it from the browser. What error do you get in the Terminal? Copy this error and then from the Amazon Q Developer Chat interface enter the following prompt, pasting the error you get in your Terminal after the hyphen "-" :

> When I run this application it generates the following error -  {your error message}

Review the output. It should help you find the issue quickly, and you now know how to fix. Fix it and try running the application again. This time create a poll and try voting. When you do this it should generate an error. Repeat the same process, using Amazon Q Developer to fix the code. This time, rather than using the Chat interface, from the editor, right click and from the "Amazon Q" menu option, select FIX and see what happens.

Review the output that is displayed in the Amazon Q Developer Chat interface. It should tell you have to resolve the issue. Once resolved, try repeating the process and voting in a poll - this time it should all work.

This short lab just touched upon the troubleshooting capabilities that can be addressed using Amazon Q Developer. As you develop your application and then deploy those application to the Cloud, you are going to generate a number of different messages. Amazon Q Developer can help you locate where those issues are likely to be and provide useful or helpful guidance. Beware though, it is not perfect and sometimes there are going to be errors where you are still going to need to revert back to traditional ways. But in most cases you are going to get quick answers to those annoying issues: typos, missing items, etc

---

**Lab1-7 Code Reference**

**Task 12**

One of the questions you might be asking yourself is as Amazon Q Developer provides code suggestions, how much of that code might come from the open source projects used to train the large language models behind it. Amazon Q Developer allows you to configure this - you can either explicityly turn off any code suggestions that match code from open source repositories, or you can leave it enabled, and Amazon Q Developer will notify you. In practice I have found that I rarely encounter this.

Check out [this very short video](https://www.youtube.com/shorts/Fmn37wGQUY8) that shows what this looks like when it does happen.

---

## Improving our Application

In this next section, we will start working to improve our application by adding new features, adding tests, and then creating documentation so that other developers and users know how to use this application.

**Lab 02-1 Exporting Poll Data to CSV files**

**Task 13**

Lets add some more features to our application. I want to be able to export the data from a Poll as a csv file. We can ask Amazon Q Developer to help us add this new capability. Up until now Amazon Q Developer has been building up context of what we have been doing, and with features like Amazon Q Developer workspace, we can make sure that it understand the existing application before making suggestions.

From the Amazon Q Developer Chat interface, we are going to use the @workspace feature again, so type @ and then select and press enter on workspace. To finish the prompt, use the following:

>@workspace I want to add a new feature in this application that exports all the data from a Poll as a csv file. How can I do this

Review the guidance. Does it look good? Follow the guidance and add the new route and make changes to the existing html files. After you have made these changes, run the application and see if you can now export the data from a poll.

If you get stuck, then you can [check out the code](https://github.com/094459/q-workshop-app/tree/lab-06) that it produced when I ran these prompts here, or look at the code directly in your IDE by switching to this branch.

```
git checkout lab-06
```

---

**Lab 02-2 Adding Tests**

We now have a working application, but what we do not have is any tests. In this lab we are going to create some, using one of the advanced features of Amazon Q Developer, the Agent for software development (or /dev). There is a bit of waiting whilst this is working, so feel free to grab a refreshment while it is running or stretch your legs!

**Task 14**

 If you are new to writing tests, we can get some hints from Amazon Q Developer in the Chat interface by typing the following prompt:

> What are the most popular Python testing frameworks that might be suitable for this project

This might be useful to help us better understand how to narrow down our choices, understand trade offs, and then let us start to write those tests. We can also get Amazon Q Developer Agent for software development to help us. By invoking this using the /dev, we can then ask it something like:

> /dev Create unit tests for this application that test registering a user, creating a poll, and voting on a poll

After we hit return, watch as Amazon Q Developer Agents get to work. This will take around 4-5 minutes again, and once complete you will get a chance to see and review the code it wants to create. You have three chances to ask Amazon Q to refine or update its response. Sometimes you need to do this - it might have missed some files, or perhaps omitted one of your requirements. When it does that, make sure you use the "Provide Feedack and Generate".


> **Note!** As of writing, using Amazon Q Developer Agent provides you with three follow up prompts you can use to help tailor the output. Why is this important? Using /dev is an advanced feature of Amazon Q Developer, and there is  limited quota when using the Builder ID and so you need to make sure that if you do use it, you use up your allocated follow ups before you use another of your allocated units of /dev. You can increase that quote by using the Professional Tier of Amazon Q Developer - this workshop however assumes you are all using the basic Builder ID version.

In my example, the test code looked ok but was using Flask test and I forgot to put in my prompt that I wanted it to use pytest. So after clicking on the "Provide Feedack and Generate" button, I enter in the prompt:

> Can you update the code so it uses pytest

This will invoke Amazon Q Developer Agent again, and it will take another 3-4 minutes as it did before. Once the Amazon Q Developer Agent for software development finishes, I get updated code that this time uses pytest. Awesome, I click on the Accept Code after a quick review and now go to try it out. I now have a test_app.py in my root folder with my tests. We can now ask Amazon Q Developer how to run this.

> @workspace how do i run the tests in test_app.py

Review the output you get. Try running the code that you generated. Does it generate any errors or do all your tests work ok? This is the fun part of working with non deterministic tools, everyone taking this workshop will most likely get subtly different outputs. If yours worked ok then great, move onto the next task.

When I ran this it told me I needed to install the pytest library with pip before I could run this, and provided me the command line text to use. Once that was installed, I tried running the test. Here is the output I got.

```
============================================================ short test summary info =============================================================
FAILED test_app.py::test_voting_success - AttributeError: 'Poll' object has no attribute 'options'
==================================================== 1 failed, 7 passed, 2 warnings in 2.10s =====================================================

```

Not too bad, but why are two tests failing. Time to use Amazon Q Developer to help us find out whats going on. This is what I enter into the chat interface

> @workspace when running the test_app.py pytest I get one failure with this error on line 63 - TypeError: object of type 'AppenderQuery' has no len()

Amazon Q Developer provides me with three options. I review, make changes and when re-running the test, it looks good.

```
================================================================ warnings summary ================================================================
test_app.py::test_voting_success
test_app.py::test_voting_success
test_app.py::test_voting_no_option_selected
test_app.py::test_voting_no_option_selected
  /Users/ricsue/Projects/amazon-q/workshop/loft/q-workshop-app/q-workshop-app/.venv/lib/python3.10/site-packages/flask_sqlalchemy/query.py:30: LegacyAPIWarning: The Query.get() method is considered legacy as of the 1.x series of SQLAlchemy and becomes a legacy construct in 2.0. The method is now available as Session.get() (deprecated since: 2.0) (Background on SQLAlchemy 2.0 at: https://sqlalche.me/e/b8d9)
    rv = self.get(ident)

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
========================================================= 8 passed, 4 warnings in 1.06s ==========================================================

```

*Using Amazon Q Developer to tweak the tests*

I have found that it is often useful to use the initial code that Amazon Q produces as a starting point, and then to make changes as needed. For example, when using /dev to create the unit tests, I found I needed to modify how it interacted with the data objects. I use Amazon Q Developer @workspace to help modify to my test needs.

In my case, the test was using the database connection from the local database, whereas I wanted it to create an ephemeral copy of the data when running tests. I used the following prompt:

> @workspace when the test is run in test_app.py, it uses the existing postgres database connection defined in app.py, and so deletes data when the test finishes. how can i change this behaviour

I was then provided information and updated code that helped me change the behaviour.


If you get stuck, then you can see the working code by checking out the [following branch](https://github.com/094459/q-workshop-app/tree/lab-07)

```
git checkout lab-07
```

---

**Lab 02-3 Adding Documentation**

Documentation is a critical part of every application, and yet sometimes this is lacking in the code and projects we have to work with. We can use Amazon Q Developer to help us automate this task, updating both documentation in code, as well as creating README files to help others understand how to use this code. Lets create some documentation for our project.

**Task 15**

We are going to do this two ways - first using @workspace to create the documentation which we will manually have to add, and then using /dev to automate the process of creating the documentation. We are first going to make sure we are all on the same page code wise:

```
git checkout lab-07
```

From a new Amazon Q Developer Chat interface, enter the following prompt:

> @workspace Add doc strings to the app.py and document how the code works, providing doc strings for each function and each route

Review the output. This is what mine looked like.

![output from using @workspace to create documentation](images/q-vscode-document.png)

I could now go through and update the code, using the "Insert Code" link that you see at the bottom of the output window. I follow this up by asking Amazon Q Developer to create me a README file, showing how the project works, how to run it, and how to use it.

> @workspace create a README file that tells readers how the project works, how to run it, and how to use it.

I was very happy with the output, but maybe there is an easier way. Well there is, and again we can use Amazon Q Developer Agent for software development (/dev) to automate this for us. We invoke /dev from the Amazon Q Developer chat interface, and then enter this prompt.

> /dev Add doc strings to the app.py and document how the code works, providing doc strings for each function and each route. Create a README.md file that tells readers how the project works, how to run it, and how to use it.

I let it run for 3-4 minutes, and after it has finished, I can review what it has done, and the output. I can see it has created a new file (README.md) and it has updated my existing app.py file.

![Amazon Q documenting my project](images/q-vscpde-readme.png)

Take a look at your output. What do you think? If you are not happy, remember to use the "Provide Feedack and Generate", and use additional prompts to tweak the documentation as you want or need it. When I ran this, I used this feedback loop to refine the README around how to create and configure the database as the initial output was not quite right (it referred to using a tool called flask db, which I did not have installed)

---

**Lab 02-4 Open Sourcing our project**

Now that my project is ready for the world to see, I have decided that I am going to open source this project as I want to build a community of people who might be interested in helping me improve the code and make it better.

**Task 16**

I can ask Amazon Q Developer to provide some guidance on what I need to do.

> **Warning!!** This guidance should be used in conjunction with conversations you have with any folk that you work with on Intelectual Property. This guidance here is only to show you how Amazon Q Developer can help you ONCE you have had those conversations and decided that open source is the way you want to go.

There are two ways I could approach this, in a similar way to the documentation. Using the native Amazon Q Developer Chat interface, or by using the Amazon Q Develoepr Agent for software development (/dev). I have decided that I am going to use @workspace, and this is the sample prompt I use:

> I want to open source this project using an Apache 2.0 licence. My company name is Beachgeek Enterprises so please update any copyright messages accordingly. How do I need to update this projects files?

I am happy with the output it provides (see below), but I think it could be improved, so I follow this up with:

> I want to include SPDX headers in the files, what do these look like

![example output of helping me open source my project](images/q-vscode-open.png)

You might need to do this if you have any specific requirements you need to meet that come out with conversations with your open source program office (OSPO) - if you have one.

Explore this and update the code.

If you get stuck, or want to see the completed sample I came up with, check out the [branch here]() or you can switch branch using the following command:

```
git checkout lab-09
```

---

**Lab 02-5 Improving our application**

Before we finish, there are a couple of final tasks that need to be done. Like many projectds we work on, we occasionally have snagging tasks that are spotted late and need to be completed before we are ready to launch. In this project there are a couple of things: First, the main page does not have a link to the about page, so we need to fix that. Second, it would be good if we could add some basic style sheets to make it look more appealing. Lets do that now.

**Task 17**

The first thing I am going to do is ask Amazon Q Developer to help me update the navigation links so they provide a link to the about page. This is the prompt I use. As you can see I am using @workspace again so that Amazon Q looks at the files in the workspace:

> @workspace can you update the project so that there is a navigation link to the about page

It provides exactly the right info. In our example we might have been able to easily update this, but when you are working in more complex projects with many hundreds of files, having this information provided will help you make those necessary changes much more quickly.

**Task 18**

Now that we have the navigation sorted, lets try and put some front end magic on this. I am going to be using @workspace again, and this is the prompt I use. Try this for yourself and then experiment a little and see how different prompts might give you different code and suggestions.

> @workspace I want to add some basic css to this project to make the Polls look more exciting. I want to add more space between the Poll options, make the button look more interesting

You will need to follow up with additional prompts. For example

> @workspace how do I update the view_results.html to use the css
> @workspace update the about.html touse the css

We could use /dev to automate and update this for us, but in this example I find it more useful to have more fine grain control on how we are changing and updating our files.


If you want to see the code that I came up with, check out [the branch here](https://github.com/094459/q-workshop-app/tree/lab-10) or switch to the branch locally using the following command

```
git checkout lab-10
```


**Task 19**

Imagine that someone had given you this project to make some changes. You are new to the code base. The documentation in the code as well as the README already provide you with some help, but what if you want more specific help.

Amazon Q Developer can help you with its integrated feature to explain how code works. From the editor, select a portion of the code (or event all of it) and right click. From the Amazon Q menu option, select "Explain" and then review the output from Amazon Q Developer in the Chat interface window. 

---

**Lab 02-6 Optimising our code**

**Task 20**

We now have our working application, delivered on time and with (fingers crossed) no significant issues. At this point, you might need to submit applications for system or load testing, to see how well your application deals with load. To make sure that our application has the best chance of passing those tests with flying colours, we can use Amazon Q Developer to help us optimise the code.

To make sure we are all on the same baseline code, check out the following branch

```
git checkout lab-10
```

Close all tabs, and then open the app.py. Find the function that generates the Yoda quotes, and select all the code. Once selected, right click, select Amazon Q and then select Refactor. Review the output and suggestions. This is what it might look like.

![optimising the code using refactor](images/q-vscode-optimise-1.png)

Repeat the process, selecting the code and this time select Optimise. Review the output and suggestions. This is what it might look like.

![optimising the code using optimise](images/q-vscode-optimise-2.png)

They provide slightly different recommendations, and this can be useful to understand how you can use this when you need one approach or the other in your code. I find it useful to run this after a new code block that I have put in (wither generated by myself, or by Amazon Q)

---

## Finish and Clean up

Once you have completed this lab, make sure you have removed any resources you do not want to keep by following these instructions

**Shutdown the Postgres database**

If you created a local Postgres database, you need to shut this down. Open the terminal session where you started Postgres and CTRL+C, and then run the following command when the command prompt returns

```
docker compose -p local-postgres -f postgres.yml down
```

You can additional delete any container images that were downloaded 


**Clean up the lab directories**

Delete the working directory we created at the beginning of this lab, which contains all the files we worked on.


## Additional resources to help you improve your Amazon Q Developer skills

I have provided some additional resources for those of you who want to dive deeper and explore more how Amazon Q Developer can help you.

* Check out [Securing Your Code With Amazon Q Developer](https://catalog.us-east-1.prod.workshops.aws/workshops/fe2c944b-f014-44d6-a243-1fc2e30b5f73/en-US/introduction) which dives deeper into how to use the Security scanning feature of 'Amazon Q Developer' to detect security policy violations and vulnerabilities in your code to help you improve it's security quality.

* Check out the [AWS Community resources](https://community.aws/amazon-q) that regularly feature new use cases, tips and tricks, and other examples of how people are using Amazon Q Developer to help simplify their flow.

* Check out AWS Community Builder Christian Bonzelet [GitHub repo](https://github.com/cremich/awesome-q-developer) where he shares a growing list of essential resources.

* I have put together another one of these self guided tutorials, this time [building a URL shortner](https://github.com/094459/q-workshop). This section also include how to deploy to AWS, and how Amazon Q Developer can help you there.


---

## Reference: Setting up a local Postgres database

If you want to run one locally, you can use the following which uses Docker Compose (or Finch if you are using that) to spin up a local Postgres database.


*Start a local Postgres database*

This lab will need a running Postgres database. We will be using Docker to get one locally up and running. If you do not have or are allowed to have Docker installed, please speak with the instructor - they will provide a suitable workaround that will allow you to connect to a Postgres database. Follow these instructions if you DO have Docker running locally. 

In this directory we have our docker compose file, which we can see provides a very simple setup for running a local PostgreSQL database.

```
version: '3'
volumes:
  psql:
services:
  psql:
    image: postgres
    environment:
      POSTGRES_USER: postgres
      POSTGRES_PASSWORD: change-me
    volumes:
      - psql:/var/lib/postgresql/data 
    ports:
      - 5432:5432 
```
Take note of the username (postgres) and password (change-me) that will get configured for this local Postgres database. It will use the standard port of 5432.

To start our Postgres database (make sure you are in the finch directory)

```
cd docker
docker compose -p local-postgres -f postgres.yaml up
```
You should see output that looks similar to the following:

```
INFO[0000] Creating network local-postgres_default      
INFO[0000] Ensuring image postgres                      
INFO[0000] Creating container local-postgres-psql-1     
INFO[0000] Attaching to logs                            
psql-1 |
psql-1 |PostgreSQL Database directory appears to contain a database; Skipping initialization
psql-1 |
psql-1 |2024-05-15 16:18:45.413 UTC [1] LOG:  starting PostgreSQL 15.6 (Debian 15.6-1.pgdg120+2) on aarch64-unknown-linux-gnu, compiled by gcc (Debian 12.2.0-14) 12.2.0, 64-bit
psql-1 |2024-05-15 16:18:45.414 UTC [1] LOG:  listening on IPv4 address "0.0.0.0", port 5432
psql-1 |2024-05-15 16:18:45.414 UTC [1] LOG:  listening on IPv6 address "::", port 5432
psql-1 |2024-05-15 16:18:45.416 UTC [1] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
psql-1 |2024-05-15 16:18:45.420 UTC [29] LOG:  database system was interrupted; last known up at 2024-05-14 13:34:27 UTC
psql-1 |2024-05-15 16:18:45.514 UTC [29] LOG:  database system was not properly shut down; automatic recovery in progress
psql-1 |2024-05-15 16:18:45.518 UTC [29] LOG:  redo starts at 0/1E4F2B8
psql-1 |2024-05-15 16:18:45.518 UTC [29] LOG:  invalid record length at 0/1E4F3A0: expected at least 24, got 0
psql-1 |2024-05-15 16:18:45.518 UTC [29] LOG:  redo done at 0/1E4F368 system usage: CPU: user: 0.00 s, system: 0.00 s, elapsed: 0.00 s
psql-1 |2024-05-15 16:18:45.521 UTC [27] LOG:  checkpoint starting: end-of-recovery immediate wait
psql-1 |2024-05-15 16:18:45.528 UTC [27] LOG:  checkpoint complete: wrote 3 buffers (0.0%); 0 WAL file(s) added, 0 removed, 0 recycled; write=0.003 s, sync=0.002 s, total=0.009 s; sync files=2, longest=0.001 s, average=0.001 s; distance=0 kB, estimate=0 kB; lsn=0/1E4F3A0, redo lsn=0/1E4F3A0
psql-1 |2024-05-15 16:18:45.531 UTC [1] LOG:  database system is ready to accept connections
```

Leave this up and running in a command window as we will need to connect to this as we build our application.

> **Stopping the local Postgres database**
>
>To stop the Postgres database, use CTRL + C
>
>```
>^CINFO[0119] Stopping containers (forcibly)               
>INFO[0119] Stopping container local-postgres-psql-1  
>```
>
> and then type the following
>
>```
>docker compose -p local-postgres -f postgres.yml down
>```
>Which will return you back to the command line.
>


