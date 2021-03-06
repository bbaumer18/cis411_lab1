# Lab Report Template for CIS411_Lab1
Course: Messiah College CIS 411, Fall 2018
Instructors: [Joel Worrall](https://github.com/tangollama) & [Trevor Bunch](https://github.com/trevordbunch)
Name: Brandon Baumer
GitHub: bbaumer18(https://github.com/bbaumer18)
Collaborators: Thomas Wood

# Step 0: Reviewing Architectural Patterns
See the [lecture / discussion](https://docs.google.com/presentation/d/1nUcy63FWPFYO3OJmERJpMjEtdaFtaIBbuUkpmNRVRas/edit#slide=id.g45345bd5ea_0_136) from CIS 411. You'll need to be familiar with the content from this lecture to complete this assignment.

Note: you are free to work with classmates on this assignment. _Good architecture is born out of collaboration - not reclusive mad-scientist behavior._ However, if you work with colleagues:

1. You must specifically note your collaborators by name at the top of your report.
2. You may not completely copy each others work (diagrams and descriptions, even if your solutions are identical).

# Step 1: MVC Architecture
Review the proposals for the Serve Central project. Let's imagine that the project has been granted (relatively) unlimited resources if they can deliver a version 1 release in 120 days. As a result, the team decides to implement an MVC architecture for its version 1 release, delivering functionality through a [responsive web application](https://en.wikipedia.org/wiki/Responsive_web_design). 

Based on the [this](https://docs.google.com/presentation/d/1UnU0xU0wF1l8pAB8trtLpdM0yuskx66jTFJzd64nsjU/edit#slide=id.g439b9c6866_2_53) and [this](https://docs.google.com/presentation/d/1-VZfAFoBVr6ijNepKAtRA7JoAQsV2Jlbf2l1WPDMhI0/edit) presentation:

1) Document two use cases of your choosing

| Use Case #1 | |
|---|---|
| Title | Volunteer can edit account information |
| Description / Steps | Volunteer can go to their account page and click on "Edit" to change the information of their profile. |
| Primary Actor | Volunteer |
| Preconditions | Volunteer already has a profile/account |
| Postconditions | Volunteer has new account information saved to their profile |

| Use Case #2 | |
|---|---|
| Title | Volunteer can look for nearby events |
| Description / Steps | Volunteer can open the map module and view their location and any events that are located near them (with their dates and times displayed) on the map.  |
| Primary Actor | Volunteer |
| Preconditions | Volunteer must have an account, have their location saved with their account information, and be on the event search page of the application |
| Postconditions | Volunteer will see a map screen with all nearby events displayed along with the date and time of each event |


2) Highlight a [table](https://www.tablesgenerator.com/markdown_tables) of at least **four models, views, and controllers** needed to produce this project.

| Model | View | Controller |
|---|---|---|
| Volunteer Class | Account Information View | Volunteer Controller |
| Event Class | Event View  | Event Controller |
| Location Class | Map View | Map Location Controller |
| Sponsor Class | Sponsor Acccount View | Sponsor Controller |

3) Generate and [embed](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#images) at least one diagram of the interaction between an Actor from the Use Cases, and one set of Model(s), View(s), and Controller(s) from the proposed architecture, including all the related / necessary services (ex: data storage and retrieval, web servers, container tech, etc.)
	- [Diagram](https://github.com/bbaumer18/cis411_lab1/blob/master/labreports/User%20Case%20Diagram.jpg)

_Note: You are free to use any diagraming tool and framework that you want as long as it clearly communicates the concept. I typically use a UML System Use Case or [UML Sequence Diagram](https://www.uml-diagrams.org/index-examples.html).  If you do not have a preferred diagramming tool: [draw.io](http://draw.io) or [lucidchart](http://lucidchart.com) are good cloud-based options._

# Step 2: Enhancing an Architecture
After an initial release and a few months of operation, Serve Central encounters a tremendous growth opportunity to extend their service and provide a volunteer recuitment and management interface to __four__ of the primary volunteer entities in the United States. As such, a reevaluation of the architecture is required, one that allows:

1. Thirdparty services to both input and retrieve data from the Serve Central model/datastore. (For instance, receiving volunteer opportunities from United Way chapters across the country.)
2. Building organization-specific interfaces on top of the Serve Central business and data logic. (For instance, allowing the registration services of Serve Central to be embedded in the website of local churches, [ah-la Stripe embedding](https://stripe.com/payments/elements).)

To support these objectives:
1. What architectural patterns (either of those presented in class on based on your own research) are appropriate? Justify your response, highlighting your presumed benefits / capabilties of your chosen architecture(s) **as well as as least one potential issue / adverse consequence** of your choice.
	- The most appropriate patterns to support these objectives would be to utilize a mix of a layered architecture with some form of Broker to distribute information. Having the broker would best enable the broad distribution of data to clients in an efficient manner. Also, having the layered architecture would allow for different presentation layers to be created and connected to the same stack of other layers. One possible adverse consequence of using this architecture is that it adds more complexity through more requirements surrounding dependency management.
2. Using your preferred diagramming tool, generate a diagram of the new Serve Central architecture that supports these two new requirements.
	- [Diagram](https://github.com/bbaumer18/cis411_lab1/blob/master/labreports/Layer%20Architecture%20Diagram.jpg)

# Step 3: Scaling an Architecture
18 months into the future, Serve Central is experiencing profound growth in the use of the service with more than 100k daily, active users and nearly 1M event registrations per month. As a result, the [Gates Foundation](https://www.gatesfoundation.org/) has funded a project to build and launch a mobile application aimed at encouraging peer-to-peer volunteer opportunity promotion and organization. 

In addition to building a new mobile application interface, the grant requires that the project prepare for the following future needs:

1. Consuming bursts of 10k+ new volunteer opportunities per hour with a latency of less than 15 seconds between submitting an opportunity and it's availability in the registration service.
2. Supporting a volunteer and event data store that will quickly exceed 50TB of data
3. Allowing authorized parties to issue queries that traverse the TB's of data stored in your datastore(s).
4. Enabling researchers to examine patterns of volunteer opportunities as a way of determining future grant investments.

What archictural pattern(s) will you employee to support each of these needs? What will the benefits and consequences be? Why are changes needed at all? Justify your answers.
- With the huge increase in data storage, I believe that the most needed change would be to implement a master slave relationship over the database servers. The reason that I believe this is needed is because with that amount of information, the only way to efficiently sort through it, to get the required latency, and enable searching through that large amount of data is through enabling a master server to distribute the tasks to the chain of available servers. This process will reduce the latency and hopefully enable quick access to the massive quantity of data. The reason that this change is required is that without implementing some form of a more efficient avenue of data usage/manipulation, the latency for accessing a database with that much information would be well to high for the required standards. The consequence of implementing this master/slave architecture is that it can create some communication instability which could cause further issues. Overall though, it would be a necessary change to fit the requirements given.

# Extra Credit
1. Create and embed a comprehensive diagram of your final architecture (i.e. one that meets all the requirements of this lab, including Step 3).
2. Augment/improve the assignment. Suggest meaningful changes in the assignment and highlight those changes in the extra credit portion of your lab report.
