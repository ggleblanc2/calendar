# Java Swing Calendar GUI

## Introduction

If you’re not familiar with Java Swing, Oracle has an excellent tutorial to get you started, [Creating a GUI With JFC/Swing](https://docs.oracle.com/javase/tutorial/uiswing/index.html). Skip the Netbeans section.

I put a calendar graphical user interface (GUI) together using Java Swing. Here’s what the GUI looks like:

![November 2020](2020-11-27.png)

The application opens in the current month, with the current day highlighted in yellow.

The controls at the top of the GUI control which month is displayed on the GUI.

The `<<` button brings the calendar back one year.

The `<` button brings the calendar back one month.

The `>` button brings the calendar forward one month.

The `>>` button brings the calendar forward one year.

You may also type a date, like your birth date, into the month, day, and year fields and left-click the `Create Calendar` button to create a calendar for that date.

## Explanation

The first thing that you do when coding a Swing GUI is to execute the `SwingUtilities` `invokeLater` method. This method ensures that the Swing components are created and executed on the [Event Dispatch Thread](https://docs.oracle.com/javase/tutorial/uiswing/concurrency/dispatch.html).

Next, I coded the names of the months and the names of the days of the week. If you want to display your calendar using a language besides English, you would change the English names to the names in the language of your choice.

If you want your week to start on a different day than Sunday, you’re also going to have to adjust the code in the `getPreviousSunday` method, as well as the name of the method.

Since the `CalendarGUI` class implements `Runnable`, we create a `JFrame` in the `run` method. The `JFrame` methods must be called in a certain order. This is the order that I use for most of my Swing applications.

We create six separate `JPanels` for the `CalendarGUI`. The date panel contains all of the GUI controls. The title panel contains the month and year title text. The calendar panel contains the actual calendar for the month. The calendar panel uses two `JPanels`, one for the days of the week and one for the days of the month. The last two `JPanels` combine the date panel and title panel into one JPanel, and combine the days of the week panel and the days of the month panel into one calendar `JPanel`.

By dividing the GUI into separate `JPanels`, we can focus on one small part of the GUI at a time and use the best [Swing layout manager](https://docs.oracle.com/javase/tutorial/uiswing/layout/visual.html) for each `JPanel`. The date panel uses a `FlowLayout`. The title panel uses a `FlowLayout`. The days of the week panel uses a `GridLayout`. The days of the month panel uses a `GridLayout`. The remaining two `JPanels` use a `BorderLayout`.

The `createDatePanel` method contains four anonymous `ActionListener` classes to move the calendar display back one year, back one month, forward one month, and forward one year. These actions are somewhat simple, so I made them anonymous classes.

The `ActionListener` for entering the date and left-clicking on the `Create Calendar` button is more complicated, so I made that ActionListener a separate class.

The `createDayLabels` method creates a grid of seven `JPanels` across and six `JPanels` down, for a total of 42 `JPanels`. We need 42 `JPanels`, because some months span parts of six weeks. Each JPanel contains one JLabel.

Here’s a recent example:

![August 2020](2020-11-27 ((1)).png)

The `createDayLabels` method doesn’t attempt to put day numbers in the `JLabels`. The `createDayLabels` method just creates blank `JLabels`. We will change the values of the `JLabels` later on.

> Generally, when creating a Swing GUI, you create the GUI using Swing components one time. If you want to change the GUI, you change the **values** of the Swing components.

Comparing the November 2020 picture of the Calendar GUI to the August 2020 picture of the Calendar GUI. we can see that none of the Swing components have changed. The **date** in the date panel, the **value** in the title panel, and the **values** in the day of the month panel have changed.

The `updateDayLabels` method updates the values of the days of the month `JLabels` and updates the title `JLabel`. The `fillDays` method actually puts the number values in the days of the month `JLabels`.
