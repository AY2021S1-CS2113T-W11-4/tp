# Developer Guide

## Table of Contents
// update later on <br>
[Introduction](#introduction) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Purpose](#purpose) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Scope](#scope) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Design Goals](#design-goals) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Maintainability](#maintainability) <br>
[Definitions](#definitions) <br>
[Setting up the project in your computer](#setting-up-the-project-in-your-computer) <br>
[Design](#design) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Technological view](#technological-overview) <br>
[Architecture](#architecture) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Project Overview](#project-overview) <br>
[Writings class family](#writings-class-family) <br>
[Filter words class family](#filter-words-class-family--word-family) <br>
[Bunny class family](#bunny-class-family) <br>
[Names class family](#names-class-family) <br>
[Product scope](#appendix-a-product-scope) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Target user profile](#target-user-profile) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Value proposition](#appendix-b-value-proposition) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[User Stories](#appendix-c-user-stories) <br>
&nbsp;&nbsp;&nbsp;&nbsp;[Non-Functional Requirements](#appendix-d-non-functional-requirements) <br>
[Instruction for manual testing](#instructions-for-manual-testing) <br>

## Introduction

### Background
Fluffle is a **desktop app for creative writers**, optimized for use via a **Command Line Interface (CLI)**. It aids users in creating and managing their writings and ideas. As a fast-typing writer, this CLI app is highly suitable for you.

### Purpose
This document specified architecture and software design decisions for the creative writing assistant, Fluffle. 

### Scope
This describes the software architecture and software design decisions for the implementation of Fluffle. The intended audience of this document is the developers, designers, and software testers of Fluffle.

### Design Goals
Our goal is to create an app which improves users’ ability of writing and creativity. Developers should work closely with CS2113T’s module instructors, who represent technical advisors and CS2101’s module instructors, who represent non-technical advisors. By adhering to these tutors’ specific requirements, which imitate industrial professional standards, beginner software engineers will be able to levitate their expertises and mindset in the process of developing and presenting a new product.

### Maintainability
With the aim of increasing maintainability of Fluffle, separated packages and classes were implemented in strict compliance with Object-oriented Programming. Since it is important to be able to easily change functionality of one class without disturbing other dependent classes, each class only serves one purpose to reduce dependency on other classes. With low coupling and high cohesion, subsequent developers can make minimal effort in maintaining Fluffle.

## Definitions

|Terminology|Explanation|
|--------|----------|
|Plot bunny|A story idea that refuses to go away until it is written down.|
|Fluffle|A fluffle is a group of bunnies.| 
|CLI|Command-line Interface. </br></br>A command-line interface (CLI) processes command to a computer program in the form of lines of text. The program in the computer will read the command and start proceeding.|
|Gradle|A build tool used for automated testing. It checks for code style violations and runs unit tests to ensure the code is functional between iterations.| 
|IntelliJ|An integrated development environment that used to write and test java code.|

## Setting up the project in your computer
**Prerequisites:**
* JDK 11
* IntelliJ IDE

<div markdown="span" class="alert alert-warning">

⚠ **Caution:**

You should follow the steps with caution. Otherwise, things will not work.
</div>

First, **fork** this repo, and **clone** the fork into your computer.

If you plan to use Intellij IDEA (highly recommended):
1. **Configure the JDK**: Follow the guide [_[se-edu/guides] IDEA: Configuring the JDK_](https://se-education.org/guides/tutorials/intellijJdk.html) to to ensure Intellij is configured to use **JDK 11**.
1. **Import the project as a Gradle project**: Follow the guide [_[se-edu/guides] IDEA: Importing a Gradle project_](https://se-education.org/guides/tutorials/intellijImportGradleProject.html) to import the project into IntelliJ IDEA.<br>
  :exclamation: Note: Importing a Gradle project is slightly different from importing a normal Java project.
1. **Verify the setup**:
   1. In IntelliJ IDEA, choose to run `Duke.main()`. Gradle will need some time to build the project at first.
   1. If your setup is correct, you should see something like below:
```
--------------------------------------------------------------
Write a story with
  ______ _        __  __ _
 |  ____| |      / _|/ _| |
 | |__  | |_   _| |_| |_| | ___
 |  __| | | | | |  _|  _| |/ _ \
 | |    | | |_| | | | | | |  __/
 |_|    |_|\__,_|_| |_| |_|\___|
--------------------------------------------------------------
Hello User! Welcome to Fluffle!
What can I do for you?
--------------------------------------------------------------
What is your name?
```

## Design

The following sections describe the high-level overview of our application, Fluffle.

### Technological overview
The Integrated Development Environment, IntelliJ, is used to develop our program. The program is written in Java, and uses Gradle for building and testing purposes. Our source code is mostly original, with some functions imported from the java.util package. The remaining packages and classes which form the structure of our program are independently developed.

### Project overview
Fluffle is built using IntelliJ and all concepts for the user interfaces, as well as the backend data management of the application, was created by our team. Due to the restrictions of the project, the main file format used for storage is .txt. We opted to save the data in the text files in a user readable format as opposed to the comma separated format as it is easier for users to directly refer to and edit their saved files.

### Architecture
The following figure describes the overall architecture of Fluffle.

![UML Fluffle class diagram](graphics/diagrams/Architecture.PNG)
<p align = "center"><i><b>Figure 1: Overview of Fluffle Architecture</b></i></p>

The design of Fluffle contains four main components:
- Writing Manager component
- Bunny Manager component
- Word Manager component
- Name Manager component

All components can be accessed by the user through Fluffle's UI. On loading Fluffle, all components will be loaded from the storage. On exiting Fluffle, all components will be saved to the storage.

### Writing Manager Component

Given below is the overall architecture of Fluffle's writing component.

![Writing Manager Component](graphics/diagrams/WritingMangerComponent.PNG)
<p align = "center"><i><b>Figure 2: Writing manager architecture</b></i></p>

In Fluffle, the writings are saved in the local hard drive text file `writings.txt`. Up to now, Fluffle can hold two types of writing: `Poem` and `Essay`. Some operations that can be done on the writings are:
- Adding writings to the database.
- Deleting writings from the database.
- Getting a reminder to continue some writings on a specific date.

### Bunny Manager Component
There are two methods for the user to load their bunny ideas into the application: loading it using the app or directly editing the `bunny.txt` data file.

#### Saving bunnies via the program commands
The bunny ideas can be loaded into Fluffle by the user using the `bunny` command. This command automatically adds these `Bunny` objects into the `bunniesList` ArrayList which can be found in the BunnyList class. the `bunny` command has separate arguments for the idea and genre so the user can easily key in the two components. 

#### Loading bunnies directly into the bunny.txt file
The user may directly edit the `bunny.txt` file, though they must be careful to edit it in the correct format similar to how the program works. Specifically for each Bunny, the program will first search for the line with the `BUNNY_IDEA_TAG` as specified in the `Tags` class and parses the idea component of the Bunny. It then searches for the line with the `BUNNY_GENRE_TAG` also specified in the `Tags` class and parses the genre component of the Bunny from there. 

A sample view of what the user might find in the bunny.txt file is as follows:

```
number of plot bunnies: 2
--------------------------------------------------------------
1.
  idea: some fantasy related idea
  genre: fantasy
--------------------------------------------------------------
2.
  idea: some random idea
  genre: none
--------------------------------------------------------------
```

Since the program only searches for the idea and genre tag, it is lenient when reading in the bunny such that if the user keys in the wrong line divider or index it can still read it in. It can excuse spacing and typo as long as each Bunny is listed with an idea tag followed by its corresponding genre tag. This makes it easy for the user to directly edit the `bunny.txt` file if they wish. It will read the file until it can no longer has a next line in `bunny.txt` to read from.

#### Usage and storage
The diagram above is describes the storage of the Bunny ideas in Fluffle. 

![Bunny Manager Component](graphics/diagrams/Bunny_manager_component.png)
<p align = "center"><i><b>Figure 3: Bunny manager architecture</b></i></p>

Transferring `Bunny` ideas from the `bunniesList` to the `bunny.txt` file via the BunnySaver:
* When the user calls the `save bunny` command from the CLI, the Bunny from bunnies list are read by `saveAllBunny` command.
* The `bunniesList` ArrayList is passed by the `commandExecutor` function in the `CommandExecutor` class.
* The `saveAllBunny` command first prints the number of `Bunny` objects found in the `bunnyList` as follows:
```
number of plot bunnies: 10
--------------------------------------------------------------
```

* The `BunnySaver` class formats the idea and genre into neatly tagged strings, numbered following their index in the ArrayList and seperated by plain line dividers as follows:
```
1.
  idea: bunny idea 1
  genre: none
--------------------------------------------------------------
2.
  idea: test idea 2
  genre: none
--------------------------------------------------------------
```

Transferring `Bunny` ideas from the `bunny.txt` to the `bunniesList` file via the BunnyLoader:
* The `BunnyLoader` class handles the loading of saved `Bunny` objects from the `bunny.txt` file into the `bunniesList`. 
* The format of each `Bunny` object should consist of an idea and genre component, even if the genre component is "none". 
* For each of the `Bunny` objects in the printed list in `bunny.txt`, the parsed idea and genre are combined to create a `Bunny` object that is then added to the `bunniesList` ArrayList and can be managed by the user using the bunny related commands.

Note that all the other functions in the bunny related classes such as `BunnyList`, `DeleteBunny`, `BunnyFilter` and `GenBunny` can also access this `bunniesList` ArrayList to perform their various functions as it is passed by reference from the `commandExecutor` function, which imports the `bunniesList` from the `BunnyList` class. Find out more [here](#bunny-class-family).

### Word Manager Component
Given below is the general architecture of our Word Manager Component.

![WordManagerComponent](graphics/diagrams/WordManagerComponent.PNG)
<p align = "center"><i><b>Figure 2: Word Manager Architecture</b></i></p>

In Fluffle, the words list is stored in the local hard drive location `data/words.txt`. 
Fluffle can hold three types of word: `Noun`, `Verb` and `Adjective`. 
The operations that can be done on the words list are:
- Viewing the words list.
- Getting three random words.
- Filtering words (by word types or by substrings).

### Name Manager Component

## Implementation

### User interaction overview
![UML sequence diagram for user interaction](graphics/diagrams/Sequence_diagram_general_command.png)

After the initial logo printing and registration step, the `main` in the `Duke` class enters a while loop, which will only exit when the `exit` command is detected. This component handles the processing of various commands in Fluffle and makes it easier for developers to add new commands without interfering with implementation of other commands.

For simplicity when the `CommandExecutor` class is referenced in later UML diagrams in this document, you may assume that it is a continuation of this diagram.

### Writing Features
#### Constitution (member classes)
WritingList: Represent the objects which are particular lists of Writings to be used in the application.

Writings: Represent the objects of the writings, created from user’s input and stored in a database as text. 

This Writings class is also the parent of 2 subclasses which are Poem and Essay.
- Poem: Represents the Writings objects which have type is Poem.
- Essay: Represents the Writings objects which have type is Essay.

User: Represents the Users registered to the System

![UML Class diagram for WritingList family](graphics/diagrams/classDiagram_WritingList.png)
<p align = "center"><i><b>Figure 3: WritingList family UML diagram</b></i></p>

The above class diagram describes the overall architecture of Writings class functionalities and associations within the scope of related classes. By checking “start”, “type” command with checkStartCommand() then checkTypeCommand() methods on that sequence respectively, the user should be able to access the process of creating and saving new writings into the database. During this process, the user has the ability of choosing their preferred type of writings(which are either poem or essay at this stage)

![UML WritingList family sequence diagram](graphics/diagrams/writingList_whileAddingWriting.png)
<p align = "center"><i><b>Figure 4: General interactions between member classes when generating a new writing</b></i></p>

**Implementation**

1. The above sequence diagram illustrate the process of adding a new writing to the database of the application. 
1. In this case, the database is created under the form of an ArrayList of Writings Objects. 
1. At the beginning, the user can start the process by typing `start` into the terminal. 
1. After that, the app will repeatededly asking the using typing in `type` for entering type decision mode.
    1. During this mode, the user will only have options between `poem` and `essay` to choose before entering the main writing's attribute.
    1. After that, the user'll go to the stage of inputing the details of the writings such as `topic`, `content`, `reminder date`.
    1. The name of `author` attribute is taken by the name that the user registered at the beginning of the session.
<br>
The main purpose of this approach is not to make the process of configuring the modes more complicated but to prevent careless typos that usually occur while flags are used to indicate too many attributes.

#### Getting reminder for writings scheduled on a specific date
This feature allows users to be reminded of which writings they should continue on a specific date.

**Implementation**

When the user keys in the command `remind DATE`, where `DATE` is the date the user wants to be reminded about in form of `dd/MM/yyyy`, the program will check the validity of the command by using `CommandChecker.extractCommandType()`. Since the command is recognized, enumeration `REMIND` is returned. Then, the program flow is as follows:

1. `WritingReminder.filterWritingsOnADate()` is called by `CommandExecutor.executeCommand()`.
1. In `WritingReminder.filterWritingsOnADate()`, the `DATE` will be parsed by `LocalDate.parse()`.
1. The Java stream is used to filter the list of writings and get which ones are scheduled for that `DATE`.
1. Private `WritingReminder.printWritingsOnADate()` will be called to print out the result.

### Word Features
Fluffle contains a word bank that stores words which are keyed in by the user, together with its meaning. The diagram
below shows the implementation of the words, as well as the word list classes in the program.

![UML Words class diagram](graphics/diagrams/Words_UML_Diagram.png)
<p align = "center"><i><b>Figure 5: Words UML Class Diagram</b></i></p>

`WordsList` is an ArrayList which stores the objects of `Words` class. Each object has the following attributes:
- `Description`: the word itself
- `Definition`: the definition of the word  
- Getters of the description and definition of the object.

Each `Words` object is further classified into `Noun`, `Verb`, or `Adjective` class, which have a getter for its type that 
identifies whether it is a `noun`, `verb`, or `adjective`.

#### Adding a `noun`
This feature allows users to add a Noun into the word bank of Fluffle. When the user adds a noun using the `noun` command,
an object of the `Noun` class is created and added into the ArrayList `WordList`.

#### Adding a `verb` 
This feature allows users to add a Verb into the word bank of Fluffle. When the user adds a verb using the `verb` command,
an object of the `Verb` class is created and added into the ArrayList `WordList`.

#### Adding an `adjective`
This feature allows users to add an Adjective into the word bank of Fluffle. When the user adds an adjective using the `adj` command,
an object of the `Adj` class is created and added into the ArrayList `WordList`.

#### Listing words
This feature allows users to list all the words that are currently stored in Fluffle.

#### Generating three random words
This feature generates three random words for the user.

#### Filtering words
This feature allows users to getting words as they wish. The diagram below shows the overall architecture of filter words functionality.

![UML Filter word class diagram](graphics/diagrams/classDiagram_FilterWords.png)
<p align = "center"><i><b>Figure 6: Filter word UML Class Diagram</b></i></p>

**Implementation**

When the user enters a `filter words` command, the program will check the validity of the command by using `CommandChecker.extractCommandType()`. Since the command is recognized, `FILTER_WORDS` will be returned. Then, the program flow is as follows:

1. `FilterExecutor.executeFilterCommand()` will be called by `CommandExecutor.executeCommand()``. 
1. In `FilterExecutor.executeFilterCommand()` method, the program will:
    1. Call `FilterType.getTypeOfFilter()` to get the filter type enumeration (`WORD_TYPE`, `STARTING_STRING` or `INCLUDING_STRING`). 
    1. Call `FilterCommandSlicer.isNewFilter()` to determine whether the user wants to continue on the last filtered list or start a new filter on an entire word list. 
    1. Check whether the user has entered a print limit using `FilterCommandSlicer.getWordPrintLimitFromFilterCommand()`. 
    1. Depending on the filter type, `FilterCommandSlicer.getTargetedWordTypes()` or `FilterCommandSlicer.getTargetedStringTags()` will be called to get an array of strings containing the word types or strings required for the filter process.
    1. The array of strings will be passed to either one of the three methods `WordsFilter.filterByType()`, `WordsFilter.filterByStartingString()` or `WordsFilter.filterByIncludedString()` to process the filtering.
    1. Call `FilterList.printFilterList()` to print out the result.

The following sequence diagram shows how the components interact with each other for the scenario where the user issues the command `filter -continue by\start limit\10 -cs -cg.`

![UML Filter word sequence diagram](graphics/diagrams/Sequence_FilterWords.png)

<p align = "center"><i><b>Figure 7: Interactions between components for the command filter -continue by\start limit\10 -cs -cg</b></i></p>

In **Figure 7** above, the flow of the program after it enters the filter process is as follows:
1. The `CommandExecutor` calls `FilterExecutor.executeFilterCommand()`.
1. In the method `executeFilterCommand`, `FilterType.getTypeOfFilter()` is called to get the filter mode, which is `START`.
1. Then, `FilterCommandSlicer.isNewFilter()`, `FilterCommandSlicer.getWordPrintLimitFromFilterCommand()`, `FilterCommandSlicer.getTargetedStringTags()` is called to check whether the program should continue on the last filter list and to get print limit as well as the strings used for filtering.
    1. The returned result of `FilterCommandSlicer.isNewFilter()` is `true`.
    1. The returned result of `FilterCommandSlicer.getWordPrintLimitFromFilterCommand()` is an integer `10`.
    1. The returned result of `FilterCommandSlicer.getTargetedStringTags()` is the array `["cs", "cg"]`
1. Since the filter type is `START`, the method `WordsFilter.filterByStartString()` class is called to execute the main filter process.
1. Filter list is printed by calling `FilterList.printFilterList()`.
1. The filter process terminates.
   
### Bunny class family overivew
![UML Bunny class diagram](graphics/diagrams/Class_diagram_bunny.png)
<p= "center"><i><b>Figure 8:  Bunny ideas UML Class Diagram</b></i></p>

The above class diagram describes the overall architecture of the bunny list functionalities. Recall that the term bunny refers to  plot ideas that have yet to be devloped. 
The above classes provide the functionality of storing such ideas in an organised manner that can easily be searched, saved and loaded.

The `BunnyList` class has the public ArrayList of bunnies `bunniesList` that is accessed by the `DeleteBunny` class method `deleteBunny` which removes a selected bunny from the `bunniesList` ArrayList. Similarly, `bunniesList` is also accessed by the `BunnyFilter` class which contains the `filterBunny` function which can filter through the list and obtain bunnies with specified keywords in the idea or the genre using the command `filter bunny i\IDEA g\GENRE`, where the user may choose to omit either the `IDEA` or the `GENRE` when running the command. 

The `BunnySaver` class accesses the `bunniesList` and overwrites the current `bunny.txt` file in the data directory, saving all `Bunny` objects into the file using the `saveAllBunny`  method. Bunny objects saved in that file can then be read by the `BunnyLoader` class and added into the `bunniesList` ArrayList each time the program is started up, which is done by calling the `loadBunnyFile` method.

The `GenBunny` class can access the `bunniesList` as well. The function `pickRandomBunny` from the `GenBunny` class first randomly generates an integer between 0 and the max number of `Bunny` idea in the `bunniesList` ArrayList. It then selects that indexed `Bunny` from the `bunniesList` and returns it to the user. This allows the user to easily choose an idea to start working on without struggling to decide which idea to use.

### Bunny command implementations

#### Adding bunny idea `bunny`
![UML BunnyList sequence diagram](graphics/diagrams/Sequence_diagram_bunny.png)
<p align = "center"><b><i>Figure 9:  Bunny list UML Sequence Diagram</i></b></p>

The user may call upon the `bunny` command to add bunnies to the list. The user input is first processed by the `extractCommandType` method from the `CommandChecker` class, and the command type detected is sent to the `executeCommand` method from the `CommandExecutor` class. The `addBunny` function is called by this method accordingly. The `addBunny` command calls the `parseSingleCharacterTaggedParamsFromUserInput` method from the `Parsers` class to extract the `idea` and `genre` arguments from the command. These are then used to create a new `Bunny` object that is then added to the `bunniesList` ArrayList. The `addBunnyMessage` method from `UI` is then called to print the message that the `Bunny` idea object has been sucessfully added to the ArrayList.

#### Listing bunny ideas `list bunny` 
This feature allows users to add a Verb into the word bank of Fluffle. When the user adds a verb using the `verb` command,
an object of the `Verb` class is created and added into the ArrayList `WordList`.

#### Filtering bunny ideas: `filter bunny`

#### Saving bunny ideas: `save bunny`

#### Deleting a bunny idea: `delete bunny`

#### Generating a random bunny idea: `random bunny`

#### Resetting the entire list of Bunny ideas: `reset bunny`

### Names class family

![Names UML Class Diagram](graphics/diagrams/classDiagram_Names.png)
<p align = "center"><i><b>Figure 10: Names UML Class Diagram</b></i></p>

The above class diagram (Figure 10) describes the overall architecture of the name list functionalities. The `Names` class has the protected ArrayList of names, `nameList`, that is accessed by the `Names` class method `getName` which randomly gets a selected name from the `nameList` ArrayList. Similarly, `nameList` is also accessed by the `Names` class which contains the `filterNames` function which can filter through the list and obtain names with specified keywords using the command `filter name <NAME>`, where the user may choose to omit the `NAME` when running the command. Similarly, `nameList` is also accessed by the `Names` class which contains the `listNames` function which displays all the names stored in the `nameList` ArrayList. This is the same as the `filterNames` function when given no input String. Similarly, `nameList` is also accessed by the `Names` class which contains the `addName` function which adds a name to the list of names stored in the `nameList` ArrayList using the command `add name <NAME>`. The `NAME` cannot be omitted. Similarly, `nameList` is also accessed by the `Names` class which contains the `deleteName` function which removes a name from the list of names stored in the `nameList` ArrayList. The command to do this is `delete name <INDEX>`. The `INDEX` cannot be omitted, and the range of the `INDEX` can be determined from the `listNames` function above.

The `NamesDB` class accesses the `nameList` and overwrites the current `Names.txt` file in the data directory, saving all String objects in `nameList` into the file using the `updateDB` method. String objects saved in that file can then be read by the `NamesDB` class and saved into the `nameList` ArrayList using the `loadDB` method. In the event of the database `Names.txt` not existing, the `NamesDB` class will create the `Names.txt` database and populate the database with 500 names using the `loadDB` method.

As shown in Figure 10, both the NamesDB class and the Names class will create the `NameException` class. This is a subclass that inherits from the `Exception` superclass and passes the exception message to the superclass. In the event of an exception, it is thrown from the methods in `NamesDB` class and `Names` class and handled by the `NameException` class.

### ClearLoader class
![ClearLoader Class sequence diagram](graphics/diagrams/ClearLoader_Sequencediagram.png)
<p align = "center"><b><i>Figure 11: Sequence diagram of Clear Loader while operating the removing method for the app's writings and words</i></b></p>

**Implementation**

1. The above diagram illustare the mechanism of manipulating objects stored in the database by adding the ability of `clear` certain unwanted subjects from the database
1. The main targets of the clearing procedure are the writings and words stored in the database as array listes
1. The process begins when commandChecker detects the command `clear` enter by the users
1. If the syntax is corrected in the form of `clear type\<TYPE_OF_OBJECT> item\<FLAG (Optional)><OBJECT_INDICATOR>`, the process begin
    1. If the `<TYPE_OF_OBJECT>` chosen by the user is `writing`, the machine is now going to consider the `<FLAG>`
        1. If there is no flag, it is detected as the order of the writings stored in the database, the process is going to clear the writings with such order stated by `<OBJECT_INDICATOR>`
        1.If the flag is `-id`, the machine is going the clear the writing with respective `id` from the database
        1. Otherwise, the command is considered as invalid (mostly in case `<OBJECT_INDICATOR>` is not an integer or leads to out of bound objects
    1. If the `<TYPE_OF_OBJECT>` chosen by the user is `word`, the machine is now goin to consider the `<FLAG>`. There are 3 cases of flags available for this mode
        1. `<FLAG>` is detected as `-noun`: Remove the corresponding item labelled by the followed `<OBJECT_INDICATOR>`
        1. `<FLAG>` is detected as `-adj`: Remove the corresponding item labelled by the followed `<OBJECT_INDICATOR>`
        1. `<FLAG>` is detected as `-verb`: Remove the corresponding item labelled by the followed `<OBJECT_INDICATOR>`
        1. Otherwise, it is considered as invalid command if the `word` with respective `type` does not exist in the database.

## Aesthetic components

### Changing line divider in Fluffle: `divider`

## Testing

If you are using IntelliJ IDEA with Gradle, there are two ways to run tests for Fluffle.

### Using JUnit test
- To run all test, in IntelliJ, right click on `test/java/seedu.duke` and choose `Run Tests in 'seedu.duke'`
- To run test on a separate package/class/method, right click on that package/class/method in `test` directory and choose `Run 'NAME'`.

### Using Gradle
- To run all test, open the terminal in IntelliJ IDEA, move to the root folder of the project and key in `gradlew clean test` for Windows (`./gradlew clean test` for Mac OS/Linux).

## Appendices

### Appendix A: Product scope
#### Target user profile

The target user group are creative writers.
* Writers who enjoy digitally typing up their works and thus can integrate using our CLI based app into their workflow.
* Writers who enjoy creating short pieces but lack the organisation to do so.
* Writers who want to improve their creative writing skills and need a proper way to achieve it.

### Appendix B: Value proposition

The application aims to provide the writer with the following services:
* Provide them with an organised way to store and select their plot ideas which may be otherwise abandoned
* Provide them with customised prompt suggestions to inspire them to write
* Provide them with a system to organise longer writing projects in a neat and logical manner to facilitate the writing of long works

### Appendix C: User Stories

|Version| As a ... | I want to ... | So that I can ...|
|--------|----------|---------------|------------------|
|v1.0|new user|see usage instructions|refer to them when I forget how to use the application|
|v1.0|user|I would like the app to have a word list|keep my list of favorite words and refer to them in my writings|
|v1.0|writer|choose the name of the character generated from the database|write without thinking a lot about my character's name|
|v1.0|writer|clear and edit the saved writings in my storage|easily change them later on|
|v1.0|writer|generate words from my word list based on word type or some substrings|find the ideas to continue my writings|
|v1.0|writer|continue to filter on my last filter list|narrow down the words I want to use|
|v1.0|writer with a lot of fleeting ideas|a place I can temporarily store all my short ideas |find them easily when I need them|
|v2.0|user|check my spelling automatically|don't spell wrongly|
|v2.0|writer|have an app that list all the statistics from my past writings|
|v2.0|user|get the inspiration from the app|improve my creative writing skills|
|v2.0|user|have a database of my writings|refer to them in the future|
|v2.0|writer who uses the filter function in v1.0|limit the filter words printed out on the screen|view them easily if the filter list has a lot of words|
|v2.0|writer who is bad at sticking to an upload schedule|be reminded by the app which pieces I need to work on next|continue to hold my writing spirit|
|v2.0|writer who frequently uses the app|save the words to local storage and load them when I start the app|save more words than usual|
|v2.0|writer facing writers block|generate a random idea from my bunny storage|warm up or brainstorms on my writings|
|v2.0|writer facing writers block|have an app that randomly generate the words|brainstorm for my writings based on those words|

### Appendix D: Non-Functional Requirements

- Should be a Command-line Interface application.
- Should work on any common Operating System (Windows, Linux or OS-X platform) as long as Java 11 is installed in the system.
- Should be user-friendly to new and expert creative writers with average typing speed.
- Should help creative writers do their tasks faster by commands rather than any other programs that uses mouses and other pointing devices.
- Should display characters in ISO basic Latin alphabet and basic numbers correctly.
- Should have local storage of editable text files (.txt).
- Should work without requiring an installer.
- Should work for single user.
- Should work without Internet connection.

### Appendix E: Instructions for manual testing
Given below are the instructions to test Fluffle manually.

#### Launch and Shutdown
Following are the instructions to launch and shutdown Fluffle

1. Verify that you have `Java11` or above version installed by typing `java --version` to your computer's terminal (Command Prompt for Windows, Terminal for MacOS)
2. Get the lastest version of **Fluffle** from [here](https://github.com/AY2021S1-CS2113T-W11-4/tp/releases/tag/v2.0).
3. Copy the file to the folder you want to use as the home folder for Fluffle.
4. Type in the terminal `java -jar duke.jar` and press Enter. If the setup is correct, you should see something like below:
```
--------------------------------------------------------------
Write a story with
  ______ _        __  __ _
 |  ____| |      / _|/ _| |
 | |__  | |_   _| |_| |_| | ___
 |  __| | | | | |  _|  _| |/ _ \
 | |    | | |_| | | | | | |  __/
 |_|    |_|\__,_|_| |_| |_|\___|
--------------------------------------------------------------
Hello User! Welcome to Fluffle!
What can I do for you?
--------------------------------------------------------------
What is your name?
```
5. After entering your name, try typing the `help` command and press Enter to get started.
6. Some example commands you can try:
    1. `noun computer d\ a smart machine`: to add a noun to your word list.
    1. `list word`: to view your word list.
7. If you want to shutdown Fluffle, use the command `exit`.

**For a more specific explanation and demonstration of the commands, visit our User Guide [here](https://ay2021s1-cs2113t-w11-4.github.io/tp/UserGuide.html).**
