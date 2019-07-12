| loio |
| -----|
| b0d7db7930f64b9399dc2b4979293873 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/b0d7db7930f64b9399dc2b4979293873.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/b0d7db7930f64b9399dc2b4979293873) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/b0d7db7930f64b9399dc2b4979293873)</div>
<!-- loiob0d7db7930f64b9399dc2b4979293873 -->

## Keep Your Views Short and Simple

The view part of your app reflects what users can see and interact with. You should use a suitable set of UI controls that match your scenario and keep things simple.

***

<a name="loiob0d7db7930f64b9399dc2b4979293873__section_fsw_51z_yfb"/>

### Use `sap.m` as the Default Namespace

Most bread-and-butter controls are located in the `sap.m` namespace, which makes it the perfect default namespace. If you want to add other controls and layouts, you can define an additional namespace. For your own namespaces, you should keep the alias short and simple as well. You will typically use it in many places, and a short alias keeps your code tidy.

```lang-xml
<mvc:View
	xmlns="sap.m"
	xmls:l="sap.ui.layout"
	xmlns:mvc="sap.ui.core.mvc">
	<App>
		<Page>
			<l:HorizontalLayout>
			...
```

-   Find out more: [Namespaces in XML Views](Namespaces_in_XML_Views_2421a2c.md)


***

<a name="loiob0d7db7930f64b9399dc2b4979293873__section_ek2_w1t_zfb"/>

### Remove Clutter From Your Views

It's easy to save a few bytes and make your code a lot cleaner:

-   Don't define properties that are set to their default values.

-   Remove unused namespace aliases.

-   Omit the `content` or `items` tag for controls that define default aggregations.

-   Use self-closing XML tags for controls that don't define any aggregations.


> Note:
> Samples may contain more code that you actually need. When you copy code from a sample, it's best to remove all properties that won't be used in your views.
> 
> 

```lang-xml
<SearchField change=".onSearch"/>
<List items="{/Products}" headerText="Search Results">
	<StandardListItem title="{Name}"/>
</List>
</Panel>
```

***

<a name="loiob0d7db7930f64b9399dc2b4979293873__section_etr_ght_zfb"/>

### Clean Up Your Aggregation Templates

If you have bound aggregations, Avoid using complex or nested controls. Remember: The template below will be repeated for every entity in your data. If the template is more complex than necessary, this may lead to performance issues at runtime and slow down your app.

```lang-xml
<List
	items={/Products}>
	<StandardListItem
		title="{Name}"
		description="{Text}"/>
```

-   Learn how: Data Binding Tutorial [Step 12: Aggregation Binding Using Templates](Step_12_Aggregation_Binding_Using_Templates_97830de.md)

-   Find out more: [Aggregation Handling in XML Views](Aggregation_Handling_in_XML_Views_19eabf5.md)


***

<a name="loiob0d7db7930f64b9399dc2b4979293873__section_r4k_bkt_zfb"/>

### Think About View Modularization Early On

Things may get a little messy as your app is growing with your requirements. Therefore, name your views semantically. If a view is getting too "heavy", you should outsource parts of it to a separate view. With XML fragments and XML composites, you can flexibly reuse parts of yor UI elsewhere.

```lang-xml
<App>
	<Page>
		<myXMLComposites:SearchPanel title="Find employees"/>
		<mvc:XMLView viewName="EmployeList"/>
	</Page>
</App>
```

-   Learn how: Walkthrough Tutorial [Step 15: Nested Views](Step_15_Nested_Views_df8c9c3.md)

-   Find out more:

-   [XML Composite Controls](XML_Composite_Controls__b83a4dc.md)

-   [Reusing UI Parts: Fragments](Reusing_UI_Parts_Fragments_36a5b13.md)

***

<a name="loiob0d7db7930f64b9399dc2b4979293873__section_dnf_hnt_zfb"/>

### Choose Clever UI Patterns

OpenUI5 offers a huge collection of feature-rich UI controls, often giving you multiple implementation choices.

Aim for the simplest possible pattern to implement your use case. For more information, see the [Samples](https://openui5.hana.ondemand.com/#/controls/), and filter for "layout". 
