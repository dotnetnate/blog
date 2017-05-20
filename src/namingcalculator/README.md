<div style="background-color:rgba(0,0,0,0.5);">
# Azure Resource Naming Calculator

The Azure Resource Naming Calculator is a a macro-enabled Excel spreadsheet that allows you to create formatting expressions to test your naming convention against resource name lengths and formatting requirements. 
</div>

### Getting Started
To get started, open the "Resource Names" tab and begin by populating the Organization Name, Project/Product Name and Name Format columns. While the first two are obvious, the Name Format is the key value of the sheet. This is what allows names to be computed based on the various components of the resource information. 

To create an expression, simply enter any text along with the replacement tokens in the format of {token} within the expression. Valid tokens include:

* productName - The name of the product or project, sourced from Resource Names!B2
* component - The name of the component, sourced from the "component" column
* organizationName - The name of the organization, sourced from Resource Names!B1
* environmentName - The full name of the environment - resolved to LookupLists!I4 and down based on the value in the Environment column.
* environmentShortCode - The short code of the environment - resolved to LookupLists!J4 and down based on the value in the Environment column.
* environmentLongCode - The long code of the environment - resolved to LookupLists!K4 and down based on the value in the Environment column.
* environmentId - The id of the environment - resolved to LookupLists!L4 and down based on the value in the Environment column.
* regionName - The full name of the region - resolved to LookupLists!A4 and down based on the value in the Azure Region column.
* regionGeo- The geo name of the region - resolved to LookupLists!B4 and down based on the value in the Azure Region column.
* regionDatacenter- The data center of the region - resolved to LookupLists!C4 and down based on the value in the Azure Region column.
* regionShortCode- The short code of the region - resolved to LookupLists!D4 and down based on the value in the Azure Region column.
* regionId- The encoded region ID - resolved to LookupLists!G4 and down based on the value in the Azure Region column.
* resourceTypeName - The full resource type name - resolved to LookupLists!N4 and down based on the value in the Azure Service column.
* resourceTypeShortCode - The resource type short code - resolved to LookupLists!O4 and down based on the value in the Azure Service column.
* resourceTypeLongCode - The resource type long code - resolved to LookupLists!P4 and down based on the value in the Azure Service column.
* resourceTypeId - The resource type id - resolved to LookupLists!R4 and down based on the value in the Azure Service column.

For example, *{component}-{environmentShortCode}* for a component named "mysvc" and in the Production environment would yield: *mysvc-p* when the name is computed.

After populating the first three values, proceed to enter resources in the grid. As you enter items, the "Remaining Characters" and "Meets Name Format" columns will be updated based on the requirements for the resource type.


### Modifying Lookup Lists (i.e. I Didn't Add Everything!)

The lists on the LookupLists tab are dynamic and will run through row 1000 in each of their respective columns. The general presumption is that if we're dealing with 1,000 item long lists, we have a bigger problem so that seemed a pretty reasonable stopping point.

In particular, you'll probably want to modify the Environments and Top Level Resource Types. In the case of the former, it's likely because yours don't match mine - simple enough. In the case of the latter, it's because this isn't an exhaustive list, lengths change, patterns change and there's certainly a possibility of patterns being entered incorrectly.

That said, to add a new "record" for each list, simply start adding rows below. The validation lists in the Resource Names column will pick it up. Also, the VLOOOKUPs that are used go down to row 1000 in each area so everything should be covered. The biggest challenge is creating the Validation Expression for the various resource types. These are simply regular expressions which you can test at [Regex 101](https://regex101.com/)  
