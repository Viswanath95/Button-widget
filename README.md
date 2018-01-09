# Button-widget
Just another repository
In this page I upload my customized button widget code

HTML:

<div class="onoffswitch">
    <input type="checkbox" name="onoffswitch" class="onoffswitch-checkbox" id="myonoffswitch" checked>
    <label class="onoffswitch-label" for="myonoffswitch">
        <span class="onoffswitch-inner"></span>
        <span class="onoffswitch-switch"></span>
    </label>
</div>

CSS:

.onoffswitch {
    position: relative; width: 90px;
    -webkit-user-select:none; -moz-user-select:none; -ms-user-select: none;
}
.onoffswitch-checkbox {
    display: none;
}
.onoffswitch-label {
    display: block; overflow: hidden; cursor: pointer;
    border: 2px solid #999999; border-radius: 20px;
}
.onoffswitch-inner {
    display: block; width: 200%; margin-left: -100%;
    transition: margin 0.3s ease-in 0s;
}
.onoffswitch-inner:before, .onoffswitch-inner:after {
    display: block; float: left; width: 50%; height: 30px; padding: 0; line-height: 30px;
    font-size: 14px; color: white; font-family: Trebuchet, Arial, sans-serif; font-weight: bold;
    box-sizing: border-box;
}
.onoffswitch-inner:before {
    content: "OFF";
    padding-right: 40px;
    background-color: #EEEEEE; color: #999999;
    text-align: right;
}
.onoffswitch-inner:after {
    content: "ON";
    padding-left: 40px;
    background-color: #34A7C1; color: #FFFFFF;
}
.onoffswitch-switch {
    display: block; width: 18px; margin: 6px;
    background: #FFFFFF;
    position: absolute; top: 0; bottom: 0;
    right: 56px;
    border: 2px solid #999999; border-radius: 20px;
    transition: all 0.3s ease-in 0s; 
}
.onoffswitch-checkbox:checked + .onoffswitch-label .onoffswitch-inner {
    margin-left: 0;
}
.onoffswitch-checkbox:checked + .onoffswitch-label .onoffswitch-switch {
    right: 0px; 
}

Settings Schema code:

{
    "schema": {
        "type": "object",
        "title": "Settings",
        "properties": {
            "initialValue": {
                "title": "Initial value",
                "type": "boolean",
                "default": false
            },
            "title": {
                "title": "Switch title",
                "type": "string",
                "default": ""
            },
            "showOnOffLabels": {
                "title": "Show on/off labels",
                "type": "boolean",
                "default": true
            },
            "retrieveValueMethod": {
                "title": "Retrieve on/off value using method",
                "type": "string",
                "default": "rpc"
            },
            "valueKey": {
                "title": "Attribute/Timeseries value key (only when subscribe for attribute/timeseries method)",
                "type": "string",
                "default": "value"
            },
            "getValueMethod": {
                "title": "RPC get value method",
                "type": "string",
                "default": "getValue"
            },
            "setValueMethod": {
                "title": "RPC set value method",
                "type": "string",
                "default": "setValue"
            },
            "parseValueFunction": {
                "title": "Parse value function, f(data), returns boolean",
                "type": "string",
                "default": "return data ? true : false;"
            },
            "convertValueFunction": {
                "title": "Convert value function, f(value), returns payload used by RPC set value method",
                "type": "string",
                "default": "return value;"
            },
            "requestTimeout": {
                "title": "RPC request timeout",
                "type": "number",
                "default": 500
            }
        },
        "required": ["requestTimeout"]
    },
    "form": [
        "initialValue",
        "title",
        "showOnOffLabels",
        {
            "key": "retrieveValueMethod",
            "type": "rc-select",
            "multiple": false,
            "items": [
                {
                    "value": "none",
                    "label": "Don't retrieve"
                },
                {
                    "value": "rpc",
                    "label": "Call RPC get value method"
                },
                {
                    "value": "attribute",
                    "label": "Subscribe for attribute"
                },
                {
                    "value": "timeseries",
                    "label": "Subscribe for timeseries"
                }
            ]
        },
        "valueKey",
        "getValueMethod",
        "setValueMethod",
        {
            "key": "parseValueFunction",
            "type": "javascript"
        },
        {
            "key": "convertValueFunction",
            "type": "javascript"
        },
        "requestTimeout"
    ]
}
