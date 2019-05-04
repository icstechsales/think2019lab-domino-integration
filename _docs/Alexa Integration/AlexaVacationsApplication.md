---
title: The Amazon Alexa Vacations skill
permalink: /docs/AlexaVacationsApplication/
---

This page provides the details about the implementation of the **Amazon ALEXA Vacation** Skill.  

<h2>Skill Description</h2>
The idea behind this skill is to allow any person from the to book her holidays based on the number of holidays she still has to enjoy. 

<h3>Typical Interaction model</h3>
The default invocation sentence for the skill is `toymakers hr`. 
-   The first thing that a user needs to do is to authenticate herself.  
    This can be done using sentences such as: `my Pin code is 1 2 3 4`, `my id is 1 2 3 4`, `I am 1 2 3 4`, `my Pin is 1 2 3 4`.  
    The important thing is that the code needs to be spelled as a 4 digit code.  
    The Skill validates the entered PIN Code against the **DemoConfig DB** and greets you by name (which it retrieved during the authentication)  

-   At this point you can check how many holidays you still have to enjoy.  
This can be done using sentences such as: `check my holiays`, `how many holidays left`, `how many vacations do I have`, `check my vacation days` ...  

-   You can then book your holidays.  
You can use sentences such as: `book my holidays from next monday for 7 days`, `I wish to reserve my holidays starting from July 15 for 10 days`, `can yu book my holidays`  
If Alexa has enough information to book the holidays, it does it by decreasing the holiday counter associated to your profile.  
If You did not specify the start date or the number of days, the Alexa will ask you to specify those values.  
Note that, when calculating the end date for your holidays, the Skill will not count weekends as working days.
![Amazon ALEXA Vacations db](../images/AlexaIntegration/Alexa-vacations-db.png)

- You end the conversation at any moment by saying `exit`.  
You can interrupt a conversation at any moment saying `cancel` 

<h3>Using the skill</h3>
Once everything is properly setup, you can interact with your skill using **any Amazon ALEXA enabled device**.  
The default invocation sentence for the skill is `toymakers hr`.  
On devices that are enabled to display the Amazon ALEXA Card, you can also enjoy a richer interface.

<h2>Pre-Requisites</h2>

1.  The implementation uses two <strong style="color: #FEC70B; background-color: black">NodeRED dominodb</strong> **Configuration Nodes**:
    1.  The First one, **Vacations DB**, refers to the <strong style="color: #FEC70B; background-color: black">DOMINO</strong> database which holds the information about user's vacations.  
    It corresponds to the `Expenses.nsf`Domino database
    1.  The Second One, **DemoConfig DB**, refers to the <strong style="color: #FEC70B; background-color: black">DOMINO</strong> database which helds the information about the  users of the Application.  
    It corresponds to the `DemoConfig.nsf`Domino database

    <strong style="color:red">Note :</strong>You need to have those two databases configured and operational in order for the **Amazon ALEXA DominoDB** Skill to properly work.  
    <strong style="color:red">Note :</strong>Please refer to the documentation for the Domino Quotes Application to retrieve the template of those two databases. 

2.  You need to have an **Amazon ALEXA Developer Account** in order to import the definition of the skill  

3.  You need to have a **NodeRED instance** that is reachable from the internet.  
Actually, it is the URL of this instance that will be required to fill the Endpoint property of the Amazon ALEXA Skill.  

4.  When installing and configuring your NodeRED instance, <strong style="color:red">do NOT FORGET</strong> to install the <strong style="color: #FEC70B; background-color: black">dominodb nodejs package</strong> [as detailed here](../info-intro/).  

5.  The NodeRED skill implementation makes a reference to a [Domino V10 logo](https://icstechsales.github.io/think2019lab-domino-integration/docs/images/dominoV10.png). This logo is retrieved from this site. Feel free to change the referene to a different image.

6.  In order for the flow to properly function, you need to remember to configure the `amazonPin` field in the **DemoConfig DB**. This **must be a 4 digit number** in order for the Amazon ALEXA Skill to properly process it.
![Amazon ALEXAPIN Code Setting](../images/AlexaIntegration/Alexa-pinCode-setting.png)

<h2>The Amazon ALEXA Skill Definition</h2>
In **your Amazon ALEXA Developer Portal**, you need:

1.  to create a new Skill.
    1.  Give it a name and select Custom  
    ![Amazon ALEXA Create Skill step 1](../images/AlexaIntegration/Alexa-importSkill-01.png)  

    1.  Do not choose any template. Instead Start from Scratch  
    ![Amazon ALEXA Create Skill step 2](../images/AlexaIntegration/Alexa-importSkill-02.png)

    1.  Once you arrive to the Build screen for your skill, go to the JSON Editor and import the Skill definition that is available [from this link](../downloads/Alexa-Think2019-Skill - Vacation.json)
    ![Amazon ALEXA Create Skill step 3](../images/AlexaIntegration/Alexa-importSkill-03.png)

    1.  Do not forget to Save the model.

2.  Once you have imported the Skill definition in **your Amazon ALEXA Developer Portal**, you need to configure the endpoint as shown here:
    ![Amazon ALEXA Developer Portal](../images/AlexaIntegration/Alexa-vacations-skill-01.png)

    <strong style="color:red">Do not forget</strong> 
    1.  to enter the URL corresponding to your NodeRED running instance where the text is blurred in the picture above.
    2.  Also add the `/vacations` string at the end of the URL as the NodeRED flow would expect to receive the inputs from Amazon ALEXA at that very endpoint.

<h2>The NodeRED Flow Definition</h2>
You need to import the relevant NodeRED flow into your NodeRED instance. You can use the [export flow available here](../downloads/Alexa-Think2019-NodeRed - Vacation.json).  
We suggest to import it in its own tab. The end result would be something like this:
![QuotesApplication NodeRed Flow](../images/AlexaIntegration/Alexa-Think2019-NodeRed - Vacation.png)
