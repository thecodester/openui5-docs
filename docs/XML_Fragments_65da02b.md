| loio |
| -----|
| 65da02badf704e03a4fd6bd4c5aba8f4 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/65da02badf704e03a4fd6bd4c5aba8f4.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/65da02badf704e03a4fd6bd4c5aba8f4) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/65da02badf704e03a4fd6bd4c5aba8f4)</div>
<!-- loio65da02badf704e03a4fd6bd4c5aba8f4 -->

## XML Fragments

OpenUI5 fragments of type XML are used in the context of XML templating to provide reuse parts for templates.

Any reference to an XML fragment is inlined by the preprocessor; that is, the reference is replaced by the fragment's XML DOM and preprocessing takes place on that DOM as well. All currently available variable names are inherited into the fragment.

**Example: XML Fragment**

```lang-xml

<core:Fragment fragmentName="sap.ui.core.sample.ViewTemplate.tiny.Field" type="XML"/>
```

The fragment name can also result from a binding, including an expression binding which evaluates to a constant. As formatter functions return strings, and not booleans, `=== 'true'` has been added in the following example:

**Example: Dynamic Fragment Name**

```lang-xml

<core:Fragment fragmentName="{= ${path: 'facet>Target', formatter: 'sap.ui.model.odata.AnnotationHelper.isMultiple'} === 'true'
    ? 'sap.ui.core.sample.ViewTemplate.scenario.TableFacet'
    : 'sap.ui.core.sample.ViewTemplate.scenario.FormFacet' }" type="XML"/>
```

**Related information**  


[XML Templating](XML_Templating_5ee619f.md)
