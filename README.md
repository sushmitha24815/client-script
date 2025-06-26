Client Scripts

Introduction

Client Scripts in ServiceNow are JavaScript snippets that run in the browser to control and enhance user interaction with forms and list views. They execute in real time as users interact with the platform, enabling dynamic UI changes, validations, and user feedback mechanisms without server calls.

Use Client Scripts Client Scripts are used to:

Enhance user experience by dynamically modifying the form based on user input.
Prevent invalid data from being submitted.
Guide user actions with alerts, confirmations, or conditional behaviors.
Modify UI elements based on user roles, form states, or field values.
Types of Client Scripts

Onload

Trigger timing - When a form is loading
Typical Use Case - Set default value, Hide/Show Fields, display messages
Onchange

Trigger timing - when a field value changes
Typical use case - validate input, update related fields dynamically
Onsubmit

Trigger timing - when the form is submitted
Typical use case - Validate mandatory fields, block submission conditionally
Oncelledit

Trigger timing - when a list cell is modified
Typical use case - Validate or respond to inline edits in list view
Key APIs in Client Scripts

g_form
Object used to manipulate form elements.

Common methods:

g_form.getValue('field_name')

g_form.setValue('field_name', 'value')

g_form.setDisplay('field_name', false)

g_form.setMandatory('field_name', true)

g_form.showFieldMsg('field_name', 'message', 'info')

g_user
Provides information about the currently logged-in user.
Common properties and methods:

g_user.name – Returns user’s name

g_user.hasRole('admin') – Checks user role

g_user.getCompanyID() – Gets the company ID

g_user.userID – Returns user ID (sys_id)

Example onChange – Highlight VIP Caller

function onChange(control, oldValue, newValue, isLoading)

{

if (isLoading || newValue == '') return;

var isVIP = g_form.getReference('caller_id', function(caller) {

if (caller.vip == 'true') {

  g_form.setDisplay('vip_banner', true);

}
});

}

View-Specific Execution

Client Scripts can be scoped to specific form views, such as:

ESS (Self-Service View)
Default view
Custom views
If a script is scoped to the ESS view, it will not run on the default or other views. This ensures view-specific behaviors. You can set the "View" field in the Client Script form accordingly.

Execution Order with Order Field

When multiple Client Scripts apply to the same table and trigger type:

Use the Order field to determine the sequence.
Lower order values execute first.
Default order is 100, but you can use intervals like 10, 20, 30 for maintainability.

Script Versions and Debugging

Scripts maintain version history for rollback and audit.
Use console.log() and browser dev tools for debugging.
"Try it" mode or Preview helps test scripts before saving.
Avoid heavy logic that slows down the browser.

Best Practices

Avoid unnecessary DOM manipulation.
Use g_form and g_user instead of direct HTML references.
Don’t write heavy logic in onLoad.
Keep scripts modular and well-commented.
Always test in multiple browsers for consistency.

Summary

Client Scripts are vital to delivering a seamless, interactive UI in ServiceNow. By leveraging g_form, g_user, and thoughtful use of triggers and view scopes, developers can greatly enhance both functionality and user experience while ensuring data integrity and business rules compliance.
