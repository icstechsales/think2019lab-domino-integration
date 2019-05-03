---
title: The Amazon Alexa QuotesDB skill
permalink: /docs/AlexaQuotesApplication/
---

This page provides the details about the implementation of the **Amazon ALEXA DominoDB** Skill.  

<h2>Pre-Requisites</h2>

1.  The implementation uses two <strong style="color: #FEC70B; background-color: black">NodeRED dominodb</strong> **Configuration Nodes**:
    1.  The First one, **Prooduction DB**, refers to the <strong style="color: #FEC70B; background-color: black">DOMINO</strong> database which holds the Quotes.  
        It corresponds to the `Quotes.nsf`Domino database
    2.  The Second One, **DemoConfig DB**, refers to the <strong style="color: #FEC70B; background-color: black">DOMINO</strong> database which helds the information about the  users of the Application.  
        It corresponds to the `DemoConfig.nsf`Domino database

    <strong style="color:red">Note :</strong>You need to have those two databases configured and operational in order for the **Amazon ALEXA DominoDB** Skill to properly work.  
    <strong style="color:red">Note :</strong>Please refer to the documentation for the Domino Quotes Application to retrieve the template of those two databases. 

2.  You need to have an **Amazon ALEXA Developer Account** in order to import the definition of the skill  

3.  You need to have a **NodeRED instance** that is reachable from the internet.  
Actually, it is the URL of this instance that will be required to fill the Endpoint property of the Amazon ALEXA Skill.  

4.  When installing and configuring your NodeRED instance, <strong style="color:red">do NOT FORGET</strong> to install the <strong style="color: #FEC70B; background-color: black">dominodb nodejs package</strong> [as detailed here](../info-intro/).

5.  In order for the flow to properly function, you need to remember to configure the `amazonPin` field in the **DemoConfig DB**. This **must be a 4 digit number** in order for the Amazon ALEXA Skill to properly process it.
![Amazon ALEXAPIN Code Setting](../images/AlexaIntegration/Alexa-pinCode-setting.png)

<h2>Using the skill</h2>
Once everything is properly setup, you can interact with your skill using **any Amazon ALEXA enabled device**.
The default invocation sentence for the skill is `sales quotes`. 

<h2>The Amazon ALEXA Skill Definition</h2>
In **your Amazon ALEXA Developer Portal**, you need:

1.  to create a new Skill.
    1.  Give it a name and select Custom  
    ![Amazon ALEXA Create Skill step 1](../images/AlexaIntegration/Alexa-importSkill-01.png)  

    2.  Do not choose any template. Instead Start from Scratch  
    ![Amazon ALEXA Create Skill step 2](../images/AlexaIntegration/Alexa-importSkill-02.png)

    3.  Once you arrive to the Build screen for your skill, go to the JSON Editor and import the Skill definition that is available [from this link](../downloads/Alexa-Think2019-Skill - Quotes App.json)
    ![Amazon ALEXA Create Skill step 3](../images/AlexaIntegration/Alexa-importSkill-03.png)

    4.  Do not forget to Save the model.

2.  Once you have imported the Skill definition in **your Amazon ALEXA Developer Portal**, you need to configure the endpoint as shown here:
    ![Amazon ALEXA Developer Portal](../images/AlexaIntegration/Alexa-quotes-skill-01.png)

    <strong style="color:red">Do not forget</strong> 
    1.  to enter the URL corresponding to your NodeRED running instance where the text is blurred in the picture above.
    2.  Also add the `/quotes` string at the end of the URL as the NodeRED flow would expect to receive the inputs from Amazon ALEXA at that very endpoint.

<h2>The NodeRED Flow Definition</h2>
You need to import the relevant NodeRED flow into your NodeRED instance. You can use the [export flow available here](../downloads/Alexa-Think2019-NodeRed - Quotes App.json).  
We suggest to import it in its own tab. The end result would be something like this:
![QuotesApplication NodeRed Flow](../images/AlexaIntegration/Alexa-Think2019-NodeRed - Quotes App.png)
