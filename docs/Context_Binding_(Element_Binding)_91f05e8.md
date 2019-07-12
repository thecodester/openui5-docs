| loio |
| -----|
| 91f05e8b6f4d1014b6dd926db0e91070 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/91f05e8b6f4d1014b6dd926db0e91070.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/91f05e8b6f4d1014b6dd926db0e91070) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/91f05e8b6f4d1014b6dd926db0e91070)</div>
<!-- loio91f05e8b6f4d1014b6dd926db0e91070 -->

## Context Binding \(Element Binding\)

Context binding \(or element binding\) allows you to bind elements to a specific object in the model data, which will create a binding context and allow relative binding within the control and all of its children. This is especially helpful in master-detail scenarios.

Let’s assume we have the following JSON data:

```lang-js
{
	"company" : {
		"name"  : "Acme Inc."
		"street": "23 Franklin St." 
		"city"  : "Claremont"
		"state" : "New Hampshire"
		"zip"	: "03301"
		"revenue": "1833990"
	}
}

```

Here’s how you would use element binding in an XML view:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input id="companyInput"
		binding="{/company}"
		value="{name}"
		tooltip="The name of the company is '{name}'"/>	
</mvc:View>
```

By setting `binding="{/company}"`, we can refer to `company` children without having to qualify the full binding path, when binding `Input` control’s properties such as the `value`. Using plain property binding, our XML view would look like this:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input id="companyInput"
		value="{/company/name}"
		tooltip="The name of the company is '{/company/name}'}"/>	
</mvc:View>
```

To define an element binding in JavaScript, for example in a controller, use the `bindElement` method on a control:

```lang-js
var oInput = this.byId("companyInput")
oInput.bindElement("/company");
oInput.bindProperty("value", "name");
```

Element binding is especially interesting for containers or layouts containing many controls that are all visualizing properties of the same model object. Here’s an XML view with a `VerticalLayout` using element binding:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<l:VerticalLayout id="vLayout"
		binding="{/company}"
		width="100%">
			<Text text="{name}" />
			<Text text="{city}" />
			<Text text="{county}" />
	</l:VerticalLayout> 
</mvc:View>
```

To realize this in JavaScript, proceed as follows in your controller:

```lang-js
var oVerticalLayout = this.getView().byId('vLayout');
oVerticalLayout.bindElement("/company");
oVerticalLayout.addContent(new Text({text: "{name}"}));
oVerticalLayout.addContent(new Text({text: "{city}"}));
oVerticalLayout.addContent(new Text({text: "{county}"})););
```

Given your XML view contains a `VerticalLayout`, it will look like this:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<l:VerticalLayout id="vLayout" 
		width="100%"/> 			 
</mvc:View>
```

***

<a name="loio91f05e8b6f4d1014b6dd926db0e91070__section_96C8BDB746E149CD964641F456C7FF93"/>

### Setting a New Context for the Binding \(Master-Detail\)

You create a new binding context for an element that is used to resolve bound properties or aggregations relative to the given path. You can use this method if the existing binding path changes or has not been provided before, for example in master-detail scenarios, as outlined below.

Let's look at the following JSON model featuring a company list:

```lang-js
{
	companies : [
		{
			name : "Acme Inc.",
			city: "Belmont",
			state: "NH",
			county: "Belknap",
			revenue : 123214125.34  
		},{
			name : "Beam Hdg.",
			city: "Hancock",
			state: "NH",
			county: "Belknap"
			revenue : 3235235235.23  
		},{
			name : "Carot Ltd.",
			city: "Cheshire",
			state: "NH",
			county: "Sullivan",
			revenue : "Not Disclosed"  
		}]
}
```

Let’s take this simple view, containing a single input control:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	<Input id="companyInput"
		 value="{name}"/>	
</mvc:View>
```

In your controller, you can now bind the input control as follows:

```lang-js
var oInput = this.byId("companyInput");
oInput.bindElement("/companies/0");
```

The XML view has bound the `value` of the input to the `name` property in the model. As the path to this property in the model is not set, this will not resolve. To resolve the binding, you use the `bindElement` method which creates a new context from the specified relative path.

To remove the current binding context, call the `unbindElement` method on the input control. By doing this, all bindings now resolve relative to the parent context again.

You can also use the `bindElement` method in conjunction with list binding. Let’s consider the following extension of our JSON data:

```lang-js
{
	regions: [
		{
			name: "Americas",
			companies : [
			{
				name : "Acme Inc.",
				zip : "03301",
				city: "Belmont",
				county: "Belknap",
				state: "NH",
				revenue : 123214125.34, 
				publ: true
			},
			{
				name : "Beam Hdg.",
				zip : "03451",
				city: "Hancock",
				county: "Sullivan",
				state: "NH",
				revenue : 3235235235.23,
				publ: true
			},
			{
				name : "Carot Ltd.",
				zip : "03251",
				city: "Cheshire",
				county: "Sullivan",
				state: "NH",
				revenue : "Not Disclosed",
				publ: false 
			}]
		},{
			name: "DACH",
			companies : [
			{
				name : "Taubtrueb",
				zip : "89234",
				city: "Ginst",
				county: "Musenhain",
				state: "NRW",
				revenue : 2525, 
				publ: true
			},
			{
				name : "Krawehl",
				zip : "45362",
				city: "Schlonz",
				county: "Humpf",
				state: "BW",
				revenue : 2342525, 
				publ: true
			}]
		}
	] 
}
```

Say we want to display companies in a `sap.m.List` control. Here’s what the XML view will look like:

```lang-xml
<mvc:View
	controllerName="sap.ui.sample.App"
	xmlns="sap.m"
	xmlns:mvc="sap.ui.core.mvc">
	  <List id=”companyList” items="{companies}">
		<items>
			<StandardListItem
	 	title="{name}"
	 	description="{city}"
			/>
		 </items>
	  </List>
</mvc:View>
```

Please note that `items="{companies}"` cannot be resolved initially, since it is a relative path. In your controller, you can now provide an element binding for the list control:

```lang-js
var oList = this.byId("companyList");
oList.bindElement("/regions/0");
```

This will display the companies for region **Americas**, while the code below displays all companies in the **DACH** region \(Germany, Austria, Switzerland\):

```lang-js
var oList = this.byId("companyList");
oList.bindElement("/regions/1");
```

***

<a name="loio91f05e8b6f4d1014b6dd926db0e91070__section_mdz_2r2_xbb"/>

### API Reference

For more information, see the API Reference for the following methods:

-   [API Reference: `sap.ui.base.ManagedObject.bindObject`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/bindObject).

-   [API Reference: `sap.ui.base.ManagedObject.getObjectBinding`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/getObjectBinding).

-   [API Reference: `sap.ui.base.ManagedObject.unbindObject`](https://openui5.hana.ondemand.com/#/api/sap.ui.base.ManagedObject/methods/unbindObject).

-   [API Reference: `sap.ui.core.Element.bindElement`](https://openui5.hana.ondemand.com/#/api/sap.ui.core.Element/methods/bindElement).

-   [API Reference: `sap.ui.core.Element.getElementBinding`](https://openui5.hana.ondemand.com/#/api/sap.ui.core.Element/methods/getElementBinding).

-   [API Reference: `sap.ui.core.Element.unbindObject`](https://openui5.hana.ondemand.com/#/api/sap.ui.core.Element/methods/unbindElement).


**Related information**  


[Tutorial Step 13: Element Binding](Step_13_Element_Binding_6c7c5c2.md)

[Binding Syntax](Binding_Syntax_e2e6f41.md)

[Formatting, Parsing, and Validating Data](Formatting,_Parsing,_and_Validating_Data_07e4b92.md)
