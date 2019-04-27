---
categories: Programming VisualStudio Tutorial
---

Where I work the bulk of my time is spent implementing Server processes, and API calls, you know, getters, setters, etc. But I've noticed that a large amount of time spent, especially when I was newer, was on writing out the exact same stuff, mainly setting up tests, which apart from a few function internals are largely the same.

So how could I fix this? Get faster at typing? Not likely, I've always been prone to stupid typos and to this day I still glance at my keyboard while typing instead of the screen \(probably why I make so many typos\). But, what we do have in Visual Studio is Item Templates, they're used all the time to put in the basics of a file rather than giving you a blank page when you ask for a new class. The standard way to use it is to hit **right click** on a project &gt; **Add** &gt; **New Item** &gt; and then select something, usually just **Class** or a **Azure Function**. Ok, so, why not just make one of these Item templates custom for what I'm doing? Take the core file structures that I keep repeating and wasting time on and automate it?

That's exactly what we're going to do, I found how to do this by reading through the [MSDN docs](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-create-item-templates?view=vs-2017) and contextualising with Stack Overflow.

### Step 1 - Building your Template code

Okay, for this step you'll want to take one of the files of code that you keep repeating, for me this was Integration and Unit tests for API calls. Tear out anything specific to this file, basically all I left was the copyright comment, the namespace, the class declaration with extension, the setup and tear down functions \(empty\), and I left an empty example test method, so it looked something like this:

```csharp
/*
* Copyright comment
*/

namespace x.y.z
{
using x;
using y;
using z;

[TestClass]
public class ClassName : Extension
{
   [TestInitialize]
    public void SetUp()
    {
    }

    [TestCleanup]
    public void TearDown()
    {
    } 
    
    [TestMethod]
    public void ApiGetCharitySummaryRun_ActionProcessTaking_ExpectedOutCome()
    {
     Assert.Fail();
    }
}
}
```

Ok, save that into your project.

In the docs I linked earlier it mentions having to replace the namespace with a parameter name. Do not worry about this, this will be handled automatically in the next step, you can go back once we're done and do more of this parameter stuff to make it fancier later, but I didn't need to.

### Step 2 - Export the Template

Next you'll want to hit **Project** &gt; **Export Template...** &gt; you'll be shown an **Export Template Wizard** &gt; select **Item Template** &gt; and make sure you have the **correct project in the dropdown**, the project you saved your template code to &gt; hit **Next** &gt; **select your template code's file** &gt; hit **Next** &gt; You can **select references** to add to your template but it's not necessary if you had them in your code &gt; hit **Next** &gt; here you can give it a name, description, icon, and change the output location, **don't change the output location** unless you have to but  you can **put what you like for the other values** \(we can change this later\) &gt;  make sure **Automatically import the template into Visual Studio** is selected &gt; hit **Finish.**

Cool, once that's done it'll open up **Users/%USERPROFILE%/Documents/Visual Studio 2017/My Exported Templates** with your template zipped up as whatever you chose to name it.  You don't need to do anything here but if you go up one to **/Visual Studio 2017** and down to **/Templates/ItemTemplates** you should see it exported to there. Go ahead and extract it, and we're done with this step.

### Step 3 - Restart Visual Studio 2017

Simple.

### Step 4 - Try it out

That should be everything, so go ahead and **right click on your project** in the **Solution Explorer** and **Add** &gt; **New Item...**, you should see your new template at the top of the list so select that and create a new file. That'l create a new file for you identical to your template code, which from now on, you never have to write again.

You can customise it a bit more form here, if you go into that file you extracted in **/ItemTemplates** you'll see your template code, with all the important bits like namespace automagically replaced with a parameter like the Microsoft docs were talking about. You can modify it here and Visual Studio will pick up the changes, you can change the .ico file to change the icon, or the settings in the .vstemplate file \(you can change the name there\).

