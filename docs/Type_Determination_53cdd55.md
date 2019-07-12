| loio |
| -----|
| 53cdd55a77ce4f33a14bd0767a293063 |

<div id="loio">

view on: [help.sap.com](https://help.sap.com/viewer/DRAFT/3237636b137e43519a20ad5513c49ccb/latest/en-US/53cdd55a77ce4f33a14bd0767a293063.html) | [demo kit nightly build](https://openui5nightly.hana.ondemand.com/#/topic/53cdd55a77ce4f33a14bd0767a293063) | [demo kit latest release](https://openui5.hana.ondemand.com/#/topic/53cdd55a77ce4f33a14bd0767a293063)</div>
<!-- loio53cdd55a77ce4f33a14bd0767a293063 -->

## Type Determination

The property binding automatically determines the appropriate type depending on the property's metadata, unless a type is specified explicitly. For example, the binding `"{DeliveryDate}"` will determine the type `sap.ui.model.odata.type.DateTimeOffset` \(assuming the metadata specifies "Edm.DateTimeOffset" for this property\), but `"{path : 'DeliveryDate', type : 'sap.ui.model.odata.type.String'}"` uses the hardcoded type `sap.ui.model.odata.type.String` instead \(and does not require metadata\). You cannot specify format options or constraints unless you also hardcode the type.

Automatic type determination will take constraints from metadata into account, namely the [OData property facets](http://docs.oasis-open.org/odata/odata/v4.0/odata-v4.0-part3-csdl.html) "MaxLength", "Nullable", "Precision" and "Scale". In addition to the OData property facets, the following OData V4 annotations are considered to set type constraints on automatic type determination:

-   `Org.OData.Validation.V1.Validation.Minimum`, `Org.OData.Validation.V1.Validation.Maximum` and `Org.OData.Validation.V1.Validation.Exclusive` are used to set the constraints `minimum`, `maximum`, `minimumExclusive` and `maximumExlusive` for `sap.ui.model.odata.type.Decimal`.

-   `com.sap.vocabularies.Common.v1.IsDigitSequence` is used to set the constraint `isDigitSequence` for `sap.ui.model.odata.type.String`.


> Note:
> Only constant expressions are supported to determine the annotation value in this case.
> 
> 

Currently, the types "Edm.Boolean", "Edm.Byte", "Edm.Date", "Edm.DateTimeOffset", "Edm.Decimal", "Edm.Double", "Edm.Guid", "Edm.Int16", "Edm.Int32", "Edm.Int64", "Edm.SByte", "Edm.Single", "Edm.String" and "Edm.TimeOfDay" are supported and mapped to the corresponding type in the namespace `sap.ui.model.odata.type`. All other types, including collections, are mapped to the generic type `sap.ui.model.odata.type.Raw` which can only be used to access the raw model value "as is", but not to convert it to a human readable representation. This allows specialized controls to work with types that would otherwise not be supported.

For more information, see the [sap.ui.model.odata.type](https://openui5.hana.ondemand.com/#/api/sap.ui.model.odata.type) and [sap.ui.model.odata.type.Raw](https://openui5.hana.ondemand.com/#/api/sap.ui.model.odata.type.Raw) API documentation in the Demo Kit.
