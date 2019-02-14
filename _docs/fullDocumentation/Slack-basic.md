---
title: Slack Basic Integration
permalink: /docs/Slack-basic/
---

This page describes the integration with Slack that has been shown during the **DOMINO 10 Launch event** in October 2018.  
The implementation is really very similar to the one for Microsoft Teams that has been introduced in the [previous section](https://icstechsales.github.io/think2019lab-domino-integration/docs/MicrosoftTeams/).  
In this section we simply highlight the differences between the two impelmentations.

<h2>The Implementation</h2>
The idea of the demo was that, once a new ToyMakers Quote was created, an event was generated for Slack; the event was represented by an **actionable event** appearing in a Slack Channel which allowed the user to either Accept or Reject the Quote.

This integration is composed of two parts:
- the first part happens <strong style="color: #FEC70B; background-color: black">inside DOMINO</strong> and is implemented via an Agent developed in Lotusscript.  
It corresponds to the part of the processing which triggers the event for the target platform (in this case Slack) informing about the New Quote that has been created in <strong style="color: #FEC70B; background-color: black">DOMINO</strong> 
- the second part happens <strong style="color: #FEC70B; background-color: black">outside DOMINO</strong> . It corresponds to the implementation of the **action** (the Approve or Reject action) from the target platform (Slack).

The NodeRED flow managing the **second part of the integration** is shown in the picture below.  
![](../images/fullDocumentation/Slack-basic-01.png)

- In the case of Slack, the URL for the endpoint **from Slack** has been defined directly in the Slack Application (as opposed to Microsoft Teams where it has been defined in the event sent by <strong style="color: #FEC70B; background-color: black">DOMINO</strong> to Teams). This is a difference between the Microsoft Teams and the Slack platforms that, clearly, does not affect the behavior of our NodeRED flow. 

- Then we added a Function Node (**Get Action and UNID**) which is meant to validate that the POST Request is bringing the *Accept* or the *Reject* actions as defined by the LotusScript agent:
![](../images/fullDocumentation/Slack-basic-02.png)  
The Body of the Function Node is very simple and looks very much like the equivalent node from the Microsoft Teams example:
![](../images/fullDocumentation/Slack-basic-03.png)  
The only noticable difference is the use of a different technique to set the `msg.DDB_itemValues` parameter:
    - in the Microsoft Teams example, `msg.DDB_itemValues` was an array of object, where each object was defined with two properties, `name` (the name of the DOMINO field to be modified) and `status`(the value to set for that field)
    - in the Slack example, `msg.DDB_itemValues`is an object where the name of the proprties for the object correspond to the name of the DOMINO field to be modified and the value of such property is the value to be set for such field. <br/> A more compact representation that has been introduced in ***V 1.0.0** of the <strong style="color: #FEC70B; background-color: black">NodeRED dominodb nodes</strong>

- 
- The remaining part of the flow is really the same as the Microsoft Teams implementation.

- It is important to note that the two <strong style="color: #FEC70B; background-color: black">NodeRED dominodb nodes</strong> that we use in this flow (and which are named **update Domino record** and **read Domino record** as in the other example), share the same **NodeRED Credentials Object (Production DB)** that we have created for the previous example.  
This shows another advatange of using the <strong style="color: #FEC70B; background-color: black">NodeRED dominodb nodes</strong>: you define the target <strong style="color: #FEC70B; background-color: black">DOMINO</strong> database once and you re-use that definition everywhere you need to refer to the same database.

That was simple right ?  
What we proved in this example was that we could really concentrate on the task of properly responding to an incoming request from Microsoft Teams; the fact that we were interacting with <strong style="color: #FEC70B; background-color: black">DOMINO</strong>  has been very much simplified by the use of two cascading <strong style="color: #FEC70B; background-color: black">NodeRED dominodb nodes</strong> without worrying at all about the complexity of how it was implemented.

<h2>Error Handling</h2>
For the sake of brevity, we did not implement a sophisticated error handling branch for this flow.

<h2>Conclusion</h2>
That was simple right ?  
What we proved in this example was that we could really concentrate on the task of properly responding to an incoming request from Microsoft Teams; the fact that we were interacting with <strong style="color: #FEC70B; background-color: black">DOMINO</strong>  has been very much simplified by the use of two cascading <strong style="color: #FEC70B; background-color: black">NodeRED dominodb nodes</strong> without worrying at all about the complexity of how it was implemented.  




