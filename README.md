# jQuery Cascading Dropdown Plugin

A simple and lighweight jQuery plugin for cascading dropdown.

## Installation

Include script after the jQuery library (unless you are packaging scripts somehow else):

```html
<script type="text/javascript" src="/path/to/jquery-cascading-dropdown.js"></script>
```

## Options

#### selectBoxes

Array of select box objects

#### Select box object properties

##### selector (string)

    selector: '.selectbox1'

Selector for select box inside parent container. (Required)

##### url (string)

    url: '/api/CompanyInfo/GetCountries'

Url to be used in Ajax request for fetching select box items. (Required)

##### textKey (string)

    textKey: 'text'

The key to be used when parsing Ajax data for select box item text. (Required)

##### valueKey (string)

    valueKey: 'value'

The key to be used when parsing Ajax data for select box item value. (Required)

##### requires (array)

    requires: ['.selectbox1']

Array of select boxes required to have value before fetching own list.

##### requireAll (boolean)

    requireAll: true

If set to true, all select boxes defined in the requires array must have a value before fetching own list.

##### paramName (string)

    paramName: 'countryId'

Required select box value parameter name used in Ajax request when fetching own list.

##### onChange (function)

    onChange: function(value) { doSomething(value); }

Function to be executed when select box value is changed. Provides new select box value.

## Example usage

```javascript
$('#menu-filter').cascadingDropdown({
    selectBoxes: [
        {
            selector: '.step1',
            url: '/api/CompanyInfo/GetCountries',
            textKey: 'text',
            valueKey: 'value',
            paramName: 'cId',
        },
        {
            selector: '.step2',
            url: '/api/CompanyInfo/GetProductAreas',
            textKey: 'text',
            valueKey: 'value',
            paramName: 'aId',
        },
        {
            selector: '.step3',
            url: '/api/CompanyInfo/GetCompanies',
            textKey: 'Name',
            valueKey: 'CompanyPageUrl',
            requires: ['.step1', '.step2'],
            requireAll: true,
            onChange: function (value) {
                window.location = value;
            }
        }
    ]
});
```