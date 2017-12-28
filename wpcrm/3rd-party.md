---
title: 3rd-party Plugins
---

{% include wpcrm_premium.html %}

**Dynamics 365 Integration Premium** provides a few extensions for other WordPress plugins and enables them to integrate with Dynamics 365.

## Contact Form 7

[Contact From 7](https://wordpress.org/plugins/contact-form-7/) allows you to capture form data on the website. Dynamics 365 Integration Premium extends upon that and allows sending this data straight to the CRM.

### Usage

After installing and activating the plugin, the Contact Form 7 tag generator will have 2 new tag types: "CRM field" and "CRM Lookup field". Most of the options will be familiar to Contact Form 7 users.

![CRM fields in the CF7 tag generator](/img/wpcrm/3rd-party_cf7-fields.jpg)

The newly added tags are:

- *CRM Field* -- represents a CRM field
- *CRM Lookup Field* -- represents a CRM lookup field

Before you start adding CRM fields to the form, you must first specify which entity this form belongs to.

1. Go to the **Additional Settings** tab.
1. Add `entity: <EntityName>` to the end of the field, where `<EntityName>` is the logical name of a CRM entity, no brackets (e.g. `contact`, `account`, `lead`, etc.)

After the form entity is configured, you can go back to the **Form** tab to add tags to the form.

#### CRM Field
 
This tag allows you to map a CF7 form control to a CRM field. Data entered in this field will end up in the corresponding CRM field.
 
 ![CRM field in the CF7 tag generator](/img/wpcrm/3rd-party_cf7-crm-field.png)

Both `msdyncrm` and `msdyncrm*` are used as CRM fields. By CF7's convention, the asterisk means that the field is required.

id
: `id` attribute value of the form control (`input`, `textarea`, etc.)<br><br>
Example: `id:foo`

class
: `class` attribute value of the form control. To set two or more classes, you may use this option multiple times.<br><br>
Example: `class:bar class:baz`

field
: Attribute name of the specified entity.<br><br>
Example: `field:emailaddress1`

placeholder
: [Placeholder text](https://contactform7.com/setting-placeholder-text/) of the form control.

default
: Default value of the form control.<br><br>
Examples:<br>
`querystring.parameter` -- will fill the control with the URL query argument "parameter".<br>
`currentuser` -- will fill the control with the current user ID. See [Authentication](/wpcrm/authentication/).<br>
`currentuser.emailaddress1` -- will fill the control with the e-mail address for the current user. See [Authentication](/wpcrm/authentication/).

The full example would look like this:

```
[msdyncrm* msdyncrm-77 id:emailaddress1 class:email field:emailaddress1 placeholder "test@example.com"]
```

#### CRM Lookup Field

This tag allows you to add entity lookup controls to a CF7 form. Lookup input will be displayed as a dropdown control with values specified either explicitly or via a CRM view.
 
`msdyncrm_lookup` and `msdyncrm_lookup*` are the tags that represent the CRM lookup field. By CF7's convention, the asterisk means that the field is required.

![CRM lookup field in the CF7 tag generator](/img/wpcrm/3rd-party_cf7-crm-lookup-field.jpg)

id
: `id` attribute value of the form control (`input`, `textarea`, etc.)<br><br>
Example: `id:foo`

class
: `class` attribute value of the form control. To set two or more classes, you may use this option multiple times.<br><br>
Example: `class:bar class:baz`

field
: Lookup attribute name of the specified entity.<br><br>
Example: `field:transactioncurrencyid`

view
: Name of the view that will populate values in the dropdown.<br><br>
Example: `view:Currency Lookup View`

values
: Map of ID/label if no view has been specified.<br><br>
Examples:<br>
`":none"` (empty label, i.e. default)<br>
`"0D9140A8-265D-E511-80E9-C4346BC516E8:Australian Dollar"`

lookuptype
: Used to restrict lookup types to a single entity.<br><br>
Example: `lookuptype:transactioncurrency`

The full example would look like this:

```
[msdyncrm_lookup msdyncrm_lookup-161 field:transactioncurrencyid view:Currency Lookup View lookuptype:transactioncurrency]
[msdyncrm_lookup msdyncrm_lookup-846 field:transactioncurrencyid ":none" "0D9140A8-265D-E511-80E9-C4346BC516E8:Australian Dollar"]
```

### Additional settings

You can specify additional settings for each contact form by adding code snippets in the specific format into the Additional Settings field in the contact form's edit screen.

entity
: Specifies the entity to create new records for.<br><br> 
Example: `entity: lead`

crm_error_message
: Message text if record creation failed.<br><br>
Example: `crm_error_message: Houston, we have a problem`

commonfield
: Field that will receive aggregated values from all form fields not bound to CRM, e.g. default CF7 tags.<br><br>
Example: `commonfield: description`

fields_map
: Allows to map non-CRM CF7 tags to CRM attributes.<br><br> 
Example: `fields_map: {your-name:firstname1}{your-email:emailaddress1}`

## Gravity Forms

[Gravity Forms](https://www.gravityforms.com/) plugin provides custom forms with a robust UI. **Dynamics 365 Integration Premium** enables Gravity Forms to create new records in CRM easily.

### Usage

1. Create a new Gravity Form or choose an existing one.
1. Navigate to the form editor.
1. Point to **Form Settings** and click **Dynamics 365 Plugin**

   ![Dynamics 365 Integration in the Gravity Forms settings menu](/img/wpcrm/3rd-party_gf-menu.png)

1. Click **Add New** to create a new feed to Dynamics 365.

   ![List of feeds in the Gravity Forms settings](/img/wpcrm/3rd-party_gf-new-feed.png)

1. Enter the **Feed Name**, select an action (create or update), and choose the entity.

   ![Dynamics 365 Integration settings for a Gravity Forms form](/img/wpcrm/3rd-party_gf-feed-settings1.png)

1. In the next section, you need to map CRM fields (on the left) to corresponding form fields (on the right).

   ![Dynamics 365 field mapping for a Gravity Forms form](/img/wpcrm/3rd-party_gf-feed-settings2.png)

1. Click **Update Settings**.