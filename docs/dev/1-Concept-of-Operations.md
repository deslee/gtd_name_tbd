# Concept of Operations

## Project Objectives

Implement a minimal, reliable and usable functional web application that provides a task management solution based on the Getting Things Done ("GTD") methodology. The main focus of the application is to provide and enforce GTD features many GTD applications are missing.

### Objective Definitions

1. The application will be **minimal**. It will be as unopinionated as possible, and follow the GTD model as strictly as possible for maximum flexibility.

2. The application will be **reliable**. Data will be persisted using Google Drive and Google Calendar. Google is considered a reliable services, and using Google API eliminates the need to write our own backend.

3. The application will be **usable**. Users will be uninhibited by UI distractions, and data will be presented as cleanly and unobtrusively as possible. The goal of the system is to make it as easy as possible to collect *tasks*, *ideas*, and *projects*. The application will also provide "hints" that instruct the User of how to best use the GTD framework. (For example, in processing the In list, the application may hint to the User that they should consider doing the next action if it takes less than 2 minutes to do it.)

### Domain Definitions

#### Basic Definitions

##### `User` 

A person using the application who understands the GTD methodology.

##### `Item`

An idea expressed as text captured by the application through user interaction. The idea may not be in the required GTD format, that is the text is not something that is actionable.

##### `List`

Is an abstract aggreagte container view of one or more `Item`s and or `List`s. It can be sorted by some `User` defined sorting process. A `List` is an abstract container that in some cases may not be curated by the `User` but rather the application based on the GTD methodology (see `Focus`). When a `List` is made known to exist to the `User` by the application it must not be abstract and have a clear purpose (see `Project`).

1. `Inbox` is a `List` that cannot be deleted and contains one or more `Item`s. These `Item`s may not be actionable in which case they are to be thrown away or rewritten. **The system will not determine if the `Item` is actionable**, however the `User` can determine this.
2. `Project` is a `User` created and defined `List` for a specific collection or two or more `Item`s. The `List` is given a name and managed by the `User`.
3. `Area` is an aggregate of one or more `List`s, `Item`s and `Project`s that are related. (Example: "Personal" and "Work")

#### `Focus`

A `Focus` is a type of `List` that is curated by the application based on the GTD methodology. A `Focus` aggreagtes tasks from the `Inbox`, `Area`, `Project` based on some aggregation method. A `Focus` can be further filtered by the `User` based on a search string or tags used by the `Item` the `Focus` contains.

1. `Today` - A Focus showing Items that are marked to complete today, are due on the current date or overdue.
2. `Next` - A Focus showing Items that are due soon.
3. `Scheduled` - A Focus showing Items that can only be started no a very specific due dates.
4. `Someday` - A Focus showing Items that have been archived for sometime in the future.
5. `Projects` - An aggregate view of Projects.
6. `Person List` - A Focus of `Item`s that are assigned and waiting on a specific person to complete. (Example: The John `Person List` contains all the `Item`s that are assigned and waiting on John.

#### Other

1. `Logbook` - An aggregate of all List, Item and Project that are completed.
2. `Trash` - All List, Item and Project that have been marked for destroy.

## Lists

The GTD framework "works" by maintaining lists, one of the most simple methods of aggregating information.

### The In List

This is the most important list in the application. The purpose of this list is to help the user capture *ideas* and *tasks* as quickly, easily, and simply as possible. The User will be encouraged to enter any idea and task that occurs to them.

#### Processing the In List

The application will make it simple and trivial for the User to process the In List.

According to the GTD framework, if the In List item is **Actionable**, the User will be encouraged to list the next *physical* and *visible* Action needed to make progress on the task.

After processing, the user may choose to promote the item to either the *Next Actions List* (which is a list of Actions that the User wants to "do ASAP), or the *Someday / Maybe List* (an auxiliary list of Actions that the User does not want in their Next Actions List)

If the item is not **Actionable**, then the User can add it to a "Some day / Maybe list" or Incubate it.

If the Action is not immediately "do-able", then the User must **Delegate** it (i.e., instruct the application to remind the User about the item in the distant future).

### The Next Actions List

This list consists of the Actions of *processed, actionable Items* that should be done *as soon as possible*.

### Someday / Maybe List

This is just an auxiliary list of Items that the User also does not wish to further proceed with the item for the time being. This list is generally thought of as a list of high level, abstract goals.

#### Example

"Learn Latin" - User might not even want to learn Latin, but it is on his or her mind, so this is the list for it.

### Waiting For List

This is a list of delegated Items. A delegated item has a date which records when it was delegated. This list consists of items which are "blocked".

#### Example

"Inform boss of the project status" - This item will be in the Waiting For List if the knowledge of the Project Status blocked by a teammate's analysis of the project, or something like that.

### Projects

A project is simply a filter/view of Items that have two or more Actions. This is what most GTD apps get wrong, as they implement Projects as contexts instead. The purpose of the Projects list is to keep track of the Items, not the Actions.

### Contexts

Contexts are simply "tags." They belong in the "Next Actions List"

### Incubation

This is an optional state of an Item which is not actionable. The User can choose a Date for this Item to appear back in the In List again, in which the Item may be actionable at that time.

#### Example

"I might want to get a haircut next month"

## Overview

The app will have a **Collection Task**, in which the User will add Items to the In List.

The app will have a **Processing Task**, in which the User will process the items in their In List. There, the User will decide whether to put the item in the Next Actions List, the Someday / Maybe List, or delegate the item. The User will also decide whether or not the item is a Project.

### Drive Integration

Data will be persisted through Google Drive. The application will obtain the credentials necessary to access the User's Drive through the OAuth2 protocol.

### Calendar Integration

The application will allow for extra "sugar", such as recording *reminder dates* and *due dates* through Google Calendar. A reminder date is a span of dates which an item will be visible to the user in a specific reminder page. A due date is a date in which a task should be completed by.

### Extra fun features

#### Location awareness

User can set a "Work" location. Items with a special designated tag (default: "Work") will be able to see the the Actions of those Items in their dashboard if they are at their "Work" location. (Question: Are we even going to have a dashboard? tbd.)

# References

[GTD in 15 minutes - A Pragmatic Gudie to Getting Things Done][0]

[0]: http://hamberg.no/gtd/
