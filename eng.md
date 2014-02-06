# Designing for Easy Interaction

> **A note from the editors:** We are pleased to present an excerpt from Chapter 
5 of [A Web for Everyone: Designing Accessible User Experiences][1] by Sarah 
Horton and Whitney Quesenbery. Use the code AWFEALA to save 20 percent when you 
buy the book from [Rosenfeld Media][2].

Success in interaction design is largely a matter of following established
patterns, so people can apply what they already know to new contexts. Using
known and well-established interactive controls goes a long way in designing for
easy interaction. There are specific considerations that will help make controls
more usable for people using assistive technologies. And there are design
considerations that make interaction more usable and enjoyable for everyone,
including people with disabilities.

## Identify and describe interactive elements

Interactive elements should be easy to distinguish from other elements on the
page. For example, links and buttons can be identified in the following ways:

* **Visually.** Links are often colored and underlined, and buttons are 
identifiable by shape.
* **In code.** Link and button markup codes distinguish these elements, making 
it possible for browsers to identify them.
* **Through interaction.** Links and buttons can show their state, such as when 
they are active, through changes in their appearance. They can also be accessed 
through the keyboard or in lists of interactive elements constructed by 
assistive technology.

Between HTML, WAI-ARIA, and features of the technology platform, there are many
options for providing accessible interactivity by using code to identify and
describe interactive elements.

## Use basic HTML codes correctly

In addition to coding interactive components, you can also describe their
function programmatically. HTML has codes that help software communicate
information about components to users.

With basic HTML, interaction is limited to links and form controls. The codes
you use to provide interaction include the attributes needed to make the
elements accessible. Implementing those elements fully, according to
specification, goes far in providing accessible interactivity. Take, for
example, a label for a text input field, as shown in Figure 5.1.

Visually, the label is related by proximity, usually appearing right before the
field. In code, the label is related using the `<label for>` element and
attribute, which programmatically connects the label with the input field. That
way software can tell the user which type of information to enter into the
field.

    <label for="firstname">First name:</label>
    <input type="text" id="firstname" />
    <label for="lastname">Last name:</label>
    <input type="text" id="lastname" />

**Figure 5.1:** *Labels are visually associated by proximity with text input 
fields. In code, labels are programmatically connected using the `<label>` 
element, the `“for”` attribute, and the input field’s `“id”` attribute making 
the connection.*

## Use WAI-ARIA for complex elements

Until recently, there was not the same built-in accessible support for complex,
page-level interaction as there is for links and forms. But that is finally
changing. With WAI-ARIA, you can identify and describe interactive elements in a
way that software can read, so it is accessible to users of assistive
technology.

For example, one interaction pattern is the “accordion” widget, which is a link
that, when clicked, expands to show hidden content (see Figure 5.2). Clicking a
second time collapses the content back to its hidden state. This pattern is
helpful for content that may not be relevant to all users. It saves precious
screen real estate, and also provides a way to learn more in context, without
jumping to different pages or scrolling through one long page.

ARIA provides codes you can use to identify and describe interactive components
like an accordion widget programmatically so that assistive technology can
communicate information about the component to users. For example, in the case
of an accordion widget, the `“aria-expanded”` attribute can be set
programmatically to “true” or “false,” depending on the state of the component.

![accordion][Figure 5.2: Example accessible accordion widget from OpenAjax Alliance]

**Figure 5.2:** *The [OpenAjax Alliance][3] provides examples and downloadable 
code for many common design patterns, including an [accessible accordion widget][4].*

ARIA is helpful for other interactions as well. For example, in the sample sign-
up form, shown in Figure 5.3, error messages are coded with the attribute
`role=“alert”` so that the helpful in-line error messages can be announced to
screen reader users.

![error][Figure 5.3: Account sign-up form error message]
 
**Figure 5.3:** *In this sample account sign-up form, alerts are identified 
programmatically using the ARIA role attribute.*

## Use features of the technology platform

When you are coding elements using programming other than HTML, you should use
the features of the technology to fully identify and describe interactive
elements. For the most part, technologies like Flash and Java have the necessary
hooks for accessibility. Those who develop using these tools just need to use
them correctly and to design so it is possible to code the interaction
accessibly.

But you should consider the ramifications carefully before moving away from
standard technologies. Is the interaction necessary to the purpose and goals of
the product? If so, can you accomplish what’s needed using standard coding?
Exhaust the possibility of using standard web technologies before you make a
commitment to a non-standard, and therefore less stable and accessible format.

## Provide accessible instructions and feedback

In Chapter 4, *Organize code for clarity and flow*, we discussed how some modes
of interaction rely on linearized access, and the code order matters because it
affects the order in which elements are presented. For example, the audio mode
of a screen reader cannot present more than one piece of information or
interactive option at a time. Interactive elements that are not sequenced
correctly can create barriers for everyone, but especially for people relying on
a linear presentation.

It’s not the details of the interaction itself that create the barrier, but how
it is structured in the code and presented to users. A simple rule of thumb is
to design the page so that any changes made after it loads the first time happen
“downstream” of the cursor.

The location in the code makes a real difference to the accessibility of forms
and error messages. For example, as a user fills in a form, the code checks each
entry to be sure it is valid. It might check to see if a username is available.
But, if feedback is displayed *above* the field, the assistive technology
doesn’t see the change, and it simply proceeds to the next field. Even worse,
some forms display error messages in a “modal” pop-up window that requires the
user to close the window before correcting the errors. With the error messages
no longer displayed, the user must try to remember the list of problems while
looking for the fields to correct.

Or it could be that, after a user submits a form, software on the server
identifies a problem with the submitted data and redisplays the form so the
errors can be corrected. In some cases, the program positions the cursor in the
field in question. Unfortunately, the error message is displayed at the top of
the page. Not only will assistive technology not see this message, but most
users won’t see it either.

So as you are designing forms, you should make sure that any interactive
feedback appears both in the code and on-screen in a way that makes sense when
linearized. Most often, this means putting the inserted feedback after the
element, so it is the next thing in the tab and reading order, as well as
marking it with an ARIA role, as shown in the sample sign-up form in Figure 5.3.

Sequencing also matters for instructions. Sometimes, forms are coded so that
instructions and labels appear after the form fields and buttons. Users (and
assistive technology) have to read ahead to determine the purpose of each field
and then backtrack to fill in the field. Be sure that the elements in a form
follow a logical sequence: identify and describe an element before the
interaction, both visually and in the code.

Instructions and labels that appear inside the field are problematic because
they disappear when the field is activated. Users who need to look at the
keyboard as they type will miss the hint entirely. Others won’t remember the
details in the instructions and labels once they are no longer displayed.

## Support keyboard interaction

The point-and-click interaction model popularized by the mouse is *not*
universally usable. Nonvisual users cannot see to point the mouse. People with
dexterity issues may find mouse operations awkward and cumbersome. Some
alternative input devices work by activating keyboard commands instead. Also,
some people find keyboard control easier, more comfortable, and more efficient
than pointing.

### Provide a logical tab order

In Chapter 4, we talked about how the code order affects linear access to web
pages in *Organize code for clarity and flow*. Code order has a significant
impact on keyboard navigation, especially when using the tab key to cycle
through actionable elements (interactive controls like buttons and links) on the
page. Tabbing is a common navigation approach for keyboard users, similar to how
mouse users will look for and click on links and controls. Keyboard users will
press the tab key repeatedly until arriving at the desired element and then
press Enter to activate the control.

With standard web pages, tab order is based on the sequence of elements in the
code order. Other formats use other methods—for example, Flash calculates tab
order based on the location of elements on the screen. In either case, it’s
important to test tab order to make sure it follows a logical progression.

While it’s possible to manually set tab order in code, the best approach is to
sequence elements appropriately, so the natural tab order works in a logical and
usable fashion.

### Don’t require point-and-click interaction

Supporting keyboard interaction doesn’t mean that you can never use complex
interactions like drag and drop. Just make sure that all interactions have an
option that does not require pointing.

Here are some things to keep in mind when designing interactions:

* **Hover:** Some devices do not support hover, such as touchscreens—hover all 
you want over a touchscreen, and nothing is going to happen! Hover actions can 
also be annoying when they are triggered inadvertently, such as when a menu is 
displayed simply because the mouse pointer crossed it on the way to another part 
of the screen. Hovers can also be distracting to people with cognitive or 
attention disabilities.
* **Select:** Using “select” to trigger actions is problematic for keyboard 
users because events are activated inadvertently as soon as they are selected. 
The best approach is to use a select/activate model of interaction, where 
elements are selected and identified, and then explicitly activated by the user. 
Using this model, you can build one interaction mode that works universally.
* **Drag and drop:** This style of interaction makes direct manipulation of 
objects easy, but typically requires a pointing device and dexterity. Instead, 
you can offer a keyboard-accessible alternative way to move items from one place 
to another (see Figure 5.5).

![Drag-and-drop][Figure 5.5: Drag-and-drop bookmarking tool requires a mouse] 

**Figure 5.5:** *This feature, collecting bookmarks for related items, requires 
a mouse to drag and drop items into the list. A simple Add button would make 
this more accessible.*

### Show which element has keyboard focus

Keyboard users also benefit from a clear indicator showing which element
currently has focus. Browser software supplies a default focus
indicator—typically a dotted outline around the element. However, keyboard
usability can be improved by using CSS to provide stronger visual cues to help
users make deliberate choices about which elements to interact with. Figure 5.6
shows an example of CSS code. Best practice is to provide the same visual cue as
provided to indicate hover—for example, when the mouse or other pointing device
is “hovering” over an element.

    a:hover, a:active, a:focus { outline: 2px solid blue }

**Figure 5.6:** *Use CSS to provide a visible outline around items that have 
keyboard focus. In this example, the same 2 pixel blue outline identifies which 
item is moused over (hover), active, or has keyboard focus.*

### Don’t trap keyboard focus

“Keyboard trap” can happen with embedded objects, such as videos, applets, and 
Flash. When the focus is trapped, users can’t get in or out of an element 
without a pointing device, like a mouse. Techniques for avoiding keyboard trap 
are dependent in large part on the technology of the embedded object. Ideally, 
entering and exiting an embedded object uses the same navigation methods as a 
web page—namely, tabbing and arrow keys. For technologies that do not support 
standard navigation, provide a keyboard option and document it so that keyboard 
users can avoid getting trapped.

## Make controls large enough to operate easily

Controls on-screen may not be three dimensional, but users still need dexterity
to operate them. Physical issues from arthritis to tremors can make it hard to
accurately use a control, but so can context like working on a crowded airplane
without enough elbow room, or even wearing gloves. People navigating the web
using a touchscreen mobile device can run into difficulty trying to, for
example, select one of a set of radio buttons, or click a submit button. Even
responsive sites may not take into account the differences in size between a
pointing device and a fingertip.

The following guidelines help make controls easy to use:

* **Minimize the fine-motor skills needed for interactive elements.** Make 
buttons and touch points large enough.
* **Space controls.** Put enough space between controls so that users don’t 
accidentally activate the wrong one.
* **Minimize the complexity of the action required.** Choose controls that do 
not require timing or managing multiple actions when possible. Watch out for 
controls like multi-level menus that require a steady hand to operate.

## Let users control the operation of the interface

Try to avoid making changes that are not triggered by an explicit user request.
For example, the “carousel” of highlighted stories on a home page typically
advances automatically, based on an estimation of time needed to get through the
content. Uncontrolled motion in an interface is distracting and impacts
comprehension. Some users need more time to take in the information, so at a
minimum, provide a way to stop the action. (See Chapter 9, “Accessible Media”
for more information about multimedia.)

A better approach is to load the first image and provide clear controls for
advancing through the stories. This applies to all moving elements, including
media such as video and audio. Don’t play media automatically. Instead, wait for
users to elect to play the media. Autoplay is not only distracting, but can also
cause problems for people in a quiet setting or using a low-bandwidth connection
to the web (such as a weak mobile phone signal).

Another common practice is opening links in a new window, usually with the
rationale that it will help users return to the originating website because they
can just close the window. Unfortunately, opening a new window starts a new
browsing history. When users navigate in this new window and try to use the back
button to return to the first website, they can’t do so because the first
website is not in the history for the programmatically opened window. Indeed,
this practice could end up having the exact opposite of the desired effect—in
that, users will not be able to find their way back.

Deciding whether to open a new window is a simple illustration of an important
principle: **Don’t take actions on behalf of users that they can already
accomplish on their own.**

People who like to open links in new windows can achieve this experience on
their own, using built-in browser controls. People who do not like opening links
in a new window cannot not use that behavior if you program it into the
interface. As designers, we need to respect the boundaries of the user
environment.

## Design for contingencies

Like the fire protection and emergency exit systems of a building, digital
products must also be built so that when something does go wrong, harmful
effects are minimized or prevented through error response and recovery.

Errors can occur on many levels. Some, like broken links or programming
glitches, are a matter of writing valid code. Others occur because of confusion
about how things work, or through simple mistakes, like clicking on the wrong
menu item when your elbow is jostled, or poking a small screen. There is no such
thing as a fail-safe system. No interface is intuitive to every user, and no
user is on target every time.

Designing for contingencies is about using design to minimize the impact of
errors and system failures when they can’t be avoided.

For example, you should support users who are submitting information, ordering a
product, or posting a comment.

* **Provide a review page.** Allow users to review their input before submitting.
* **Give options for editing the submission.** Support an iterative review/edit 
process to give users plenty of time and opportunity to be certain about their 
submission.
* **Provide a confirmation page.** When the information is submitted, confirm 
the transaction and provide instructions about making any additional changes. 
Confirmation pages not only provide a nice ending to the interaction, but they 
also work as conversation:

> **User:** I’d like to place an order. Here’s all my information.

> **Your site:** Thanks. Got it. We’ll send this to you within three days.

Good communication can also make the system easier to operate and to avoid
errors. For example, if the system requires a specific date format, provide an
example date right before the input field.

If an error does occur, provide helpful and accessible feedback in response to
input errors. The feedback should appear with the element containing the error,
and should provide clear instructions for how to correct the input, as shown in
the sample sign-up form in Figure 5.3.

## Allow users to request more time

Time is a challenge for many people. It may take more time for someone using
assistive technologies, such as a screen reader, text enlarger, or alternative
input device like a joystick. They may read more slowly or need more time to
think about what they are reading. Other people need time to simply move their
muscles, and it may take a long time to get their arm and hand to coordinate to
interact with a link, button, or field. Time-outs can ruin their experience.

Some websites have features that are triggered by time—a common example is the
timeout feature used for security reasons by many web applications. When a user
logs into the system, the system notes the time and watches the activity. If a
predetermined time passes with no activity from the user, the system times out
and logs the user off.

A well-designed timeout process alerts users prior to logging them off, and
provides them with the option to continue the session. Also, if the system ends
up indeed logging off the user, it caches whatever activity they had initiated
in the browser. This allows the user to log back in and pick up where they left
off.

[1]: http://rosenfeldmedia.com/books/a-web-for-everyone/
[2]: http://rosenfeldmedia.com/
[3]: http://www.oaa-accessibility.org/
[4]: http://www.oaa-accessibility.org/examplep/accordian1/

[Figure 5.2: Example accessible accordion widget from OpenAjax Alliance]: img/389_fig52.png
[Figure 5.3: Account sign-up form error message]: img/389_fig53.png
[Figure 5.5: Drag-and-drop bookmarking tool requires a mouse]: img/389_fig55.png