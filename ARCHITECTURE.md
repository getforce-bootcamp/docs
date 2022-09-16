## Separation of Concerns
Software, like hairstyles, is often referred to as a living thing that changes and evolves over time. From the single-celled amoeba of a "Hello World" program, to the complexity of enterprise-level software, the range and variety in life also occurs in software. Complex organisms evolve systems for specialized purposes. Skeletons, muscles, and organs work as a unit, but they also interface with other systems to benefit the whole. [[Source]](https://trailhead.salesforce.com/content/learn/modules/apex_patterns_sl/apex_patterns_sl_soc)

## Trigger Framework (Domain Layer)
In our projects, we use [Trigger Framework](https://github.com/kevinohara80/sfdc-trigger-framework) for writing our triggers, because of [several reasons](https://trailhead.salesforce.com/content/learn/modules/success-cloud-coding-conventions/implement-frameworks-sc).
This trigger framework bundles a single `TriggerHandler` base class that you can inherit from in all of your trigger handlers. The base class includes context-specific methods that are automatically called when a trigger is executed.

To create a trigger handler, you simply need to create a class that inherits from TriggerHandler.cls. Here is an example for creating an Opportunity trigger handler.

```Apex
public class OpportunityTriggerHandler extends TriggerHandler {
```
In your trigger handler, to add logic to any of the trigger contexts, you only need to override them in your trigger handler. Here is how we would add logic to a beforeUpdate trigger.

```Apex
public class OpportunityTriggerHandler extends TriggerHandler {
  private List<Opportunity> newOpportunityList;
  private List<Opportunity> oldOpportunityList;
  private Map<Id, Opportunity> newOpportunityMap;
  private Map<Id, Opportunity> oldOpportunityMap;

  public OpportunityTriggerHandler() {
      this.newOpportunityList = (List<Opportunity>) Trigger.new;
      this.oldOpportunityList = (List<Opportunity>) Trigger.old;
      this.newOpportunityMap = (Map<Id, Opportunity>) Trigger.newMap;
      this.oldOpportunityMap = (Map<Id, Opportunity>) Trigger.oldMap;
  }
    
  public override void beforeUpdate() {
    OpportunityService.callMethod(oldOpportunityMap, newOpportunityMap);
  }
}
```
To use the trigger handler, you only need to construct an instance of your trigger handler within the trigger handler itself and call the run() method. Here is an example of the Opportunity trigger.

```Apex
trigger OpportunityTrigger on Opportunity (before insert, before update) {
  new OpportunityTriggerHandler().run();
}
```
TriggerHandler is [Domain layer](https://trailhead.salesforce.com/content/learn/modules/apex_patterns_dsl/apex_patterns_dsl_learn_dl_principles) of our application based on Apex Enterprise Patterns. The Apex Domain class is consumed by the Apex trigger handler and Apex service.

<p align="center"><img width="500" alt="demo" src="https://user-images.githubusercontent.com/89274213/190668809-5ce1505c-1f7c-424a-9d98-3a3bdc04bc74.png"></p>

### Important info!
Create only **one** trigger, **one** triggerhandler and **one** service classes per one object. If there is already created classes for object, which you want to implement trigger - you should just extend the existing classes.

## Service Layer
The [Service layer](https://trailhead.salesforce.com/content/learn/modules/apex_patterns_sl/apex_patterns_sl_learn_sl_principles) helps you form a clear and strict encapsulation of code implementing business tasks, calculations and processes. Each sObject has single Service class, which will be extended by additional logic. TriggerHandlers consumes all logic from Service layer and don't contain any logic.

<p align="center"><img width="500" alt="demo" src="https://user-images.githubusercontent.com/89274213/190670906-ccc6b802-de61-4bd1-bb74-27539cbc9ca8.png"></p>
