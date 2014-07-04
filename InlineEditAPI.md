Inline Edit API
===============

Inline Edit

Inline Edit allows a user to do quick edits to simple text without having to switch modes or screens. All work is done on the same interface, which helps the user maintain context.

The basic form of the Inline Edit component is the Simple Text Inline Edit. Three specific integrations are also available:

    a Dropdown Inline Edit
    a Rich Text Inline Edit using the CKEditor
    a Rich Text Inline Edit using TinyMCE

Simple Text Inline Edit
fluid.inlineEdit(container, options);
fluid.inlineEdits(container, options);

Creates an Inline Edit component (or multiple components) that uses a simple input field for the edit mode. See Simple Text Inline Edit API for details.
Dropdown Inline Edit
fluid.inlineEdit.dropdown(container, options);

Creates an Inline Edit component that uses a dropdown selection box for the edit mode. See Dropdown Inline Edit API for details.
Rich Text Inline Edit
fluid.inlineEdit.CKEditor(container, options);
fluid.inlineEdit.tinyMCE(container, options);

Creates an Inline Edit component that uses a rich text editor for the edit mode. See Rich Text Inline Edit API for details.

Supported Events

The Inline Edit component fires the following events (for more information about events in the Infusion Framework, see Events):

afterInitEdit

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

default

Parameters
    

editor
the instance of the editor component
afterInitEdit

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

default

Parameters
    

none
onCreateEditView

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

default

Parameters
    

model
The current (new) value of the "model" structure representing the editable state of the component

oldModel
A snapshot of the old value of the model structure before the current edit operation started

source
An arbitrary object which optionally represents the "source" of the change, which can be checked by listeners to prevent cyclic events. Can often be undefined.
modelChanged

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

default

Parameters
    

none
onBeginEdit

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

preventable

Parameters
    

none
onFinishEdit

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

default

Parameters
    

newValue
see parameters for modelChanged (model, oldModel)

oldValue
see parameters for modelChanged (model, oldModel)

editNode
A DOM node which holds the concrete editable control - this may vary in interpretation for different embodiments of the InlineEdit control but may, for example be an <input>, <textarea> or <select> node

viewNode
A DOM node which holds the read-only representation of the editable value.
afterFinishEdit

Description
    

This event fires when the UI Options component has been rendered and is ready for use.

Type
    

preventable

 Parameters
    

ewValue
see parameters for modelChanged (model, oldModel)

oldValue
see parameters for modelChanged (model, oldModel)

editNode
A DOM node which holds the concrete editable control - this may vary in interpretation for different embodiments of the InlineEdit control but may, for example be an <input>, <textarea> or <select> node

viewNode
A DOM node which holds the read-only representation of the editable value.
Functions

These functions are defined on the central component  object returned from the inlineEdit creator function - for example with
var myEdit = fluid.inlineEdit(componentContainer, options);
myEdit.edit();

Switches the component into edit mode. The events onBeginEdit and afterBeginEdit will fire.
myEdit.finish();

Switches the component out of edit mode into display mode, updating the displayed text with the current content of the edit field. The events onFinishEdit and afterFinishEdit will fire. If the model value has changed, there will be a call to modelUpdated in between these calls.
myEdit.cancel();

Cancels the in-progress edit and switches back to view mode.
myEdit.isEditing();

Determines if the component is currently in edit mode: Returns true if edit mode is shown, false if view mode is shown.
myEdit.refreshView(source);

Updates the state of the inline editor in the DOM, based on changes that may have happened to the model. source is an optional source object identifying the source of the change (see ChangeApplier documentation)
myEdit.tooltipEnabled();

Returns a boolean indicating whether or not the tooltip is enabled.
/**
  * Pushes external changes to the model into the inline editor, refreshing its
  * rendering in the DOM. The modelChanged event will fire.
  *
  * @param {String} newValue The bare value of the model, that is, the string being edited
  * @param {Object} source An optional "source" (perhaps a DOM element) which triggered this event
  */
myEdit.updateModelValue(newValue, source);

Updates the component's internal representation of the text to a new value. If the value differs from the existing value, the modelChanged event will fire and the component will be re-rendered.
/**
  * Pushes external changes to the model into the inline editor, refreshing its
  * rendering in the DOM. The modelChanged event will fire.
  *
  * @param {Object} newValue The full value of the new model, that is, a model object which
  *      contains the editable value as the element named "value"
  * @param {Object} source An optional "source" (perhaps a DOM element) which triggered this event
  */
myEdit.updateModel(newValue, source);

Similar to updateModelValue, only accepts specification of the overall model object (housing the editable value under the key value).
myEdit.model

Not a function, but a data structure. This directly represents the "model" or state of the editable component. External users should consider this structure as read-only, and only make modifications through the updateModel call above.

Options

The following options to the creator functions can be used to customize the behaviour of the Inline Edit component:
 
selectors
strings
listeners
styles
paddings
applyEditPadding
submitOnEnter
displayModeRenderer
editModeRenderer
displayAccessor
displayView
editAccessor
editVIew
lazyEditView
blurHandlerBinder

Description
    

A function which acts on the overall component to bind a handler for the blur event received on the editable view. For integrations where the editable view is a complex collection of elements, such as dropdown inlineEdit, this needs to take an arbitrary form. A standard implementation is provided as fluid.deadMansBlur which will infer that focus is leaving a set of elements if none of them receives a focus after a blur within a 150 millisecond horizon.

Default
    

null

Example
    
fluid.inlineEdit("#myContainer", {
    blurHandlerBinder: ""
});
selectOnEdit

Description
    

Indicates whether or not to automatically select the editable text when the component switches into edit mode.

Default
    

false

Example
    
fluid.inlineEdit("#myContainer", {
    selectOnEdit: true
});
defaultViewText

Description
    

The default text to use when filling in an empty component. Set to empty to suppress this behaviour.

Default
    

"Click here to edit"

Example
    
fluid.inlineEdit("#myContainer", {
    defaultViewText: ""
});
useTooltip

Description
    

Indicates whether or not the component should display a custom ("invitation") tooltip on mouse hover

Default
    

false

Example
    
fluid.inlineEdit("#myContainer", {
    useTooltip: true
});
tooltipText

Description
    

The text to use for the tooltip to be displayed when hovering the mouse over the component

Default
    

"Click item to edit"

Example
    
fluid.inlineEdit("#myContainer", {
    tooltipText: "Click to edit"
});

See also
    

useTooltip
tooltipID

Description
    

The id to be used for the DOM node holding the tooltip

Default
    

"tooltip"

Example
    
fluid.inlineEdit("#myContainer", {
    tooltipID: "myTooltip"
});

See also
    

useTooltip
tooltipDelay

Description
    

The delay, in ms, between starting to hover over the component and showing the tooltip

Default
    

1000

Example
    
fluid.inlineEdit("#myContainer", {
    tooltipDelay: 500
});

See also
    

useTooltip
Additional options for Multiple Inline Edits

The options for the creation of multiple Inline Edits are the same as those for the creation of a single Inline Edit, with the addition of a selector for identifying the editable elements. The default selector is defined as follows:
selectors: {
    editables: ".flc-inlineEditable"
}
InlineEdit Types

Several of the InlineEdit configuration elements make use of various "Implicit" or "Duck Typed" objects which have particular structures or signatures.
Type name
    
Description
    
Layout
ViewAccessor    Appears as displayAccessor and editAccessor. Used to convey updates to and from the model to its representation in the DOM. Exposes a single function value with the same semantics as jQuery.val().    value: function( [optional value]) }
InlineEditView  Appears as displayView and editView. Used to wrap the action of the relevant ViewAccessor as it maintains synchrony between the model and DOM. For some views, especially where there is some "default text" to invite the user to edit, there is extra formality to displaying the model which is InlineEdit-specific, rather than markup-specific. Such logic goes in this class, and is less frequently user-configured. { refreshView: function (that, source) }
InlineEditRenderer  Appears as editModeRenderer. Actually a function, rather than a structure, with a fairly complex contract. Is passed the entire component that in order to inspect the current markup situation at startup time, to manipulate it if necessary to render and initialise the editable component view, and return the relevant nodes which it has either created or discovered.   function (that) -> { container, field }

Dependencies

The Inline Edit dependencies can be met by including the MyInfusion.js file in the header of the HTML file:
<script type="text/javascript" src="MyInfusion.js"></script>

Alternatively, the individual file requirements are:

<script type="text/javascript" src="lib/jquery/core/js/jquery.js"></script>
<script type="text/javascript" src="lib/jquery/ui/js/jquery.ui.core.js"></script>
<script type="text/javascript" src="lib/jquery/ui/js/jquery.ui.widget.js"></script>
<script type="text/javascript" src="lib/jquery/ui/js/jquery.ui.position.js"></script>
<script type="text/javascript" src="lib/jquery/plugins/tooltip/js/jquery.ui.tooltip.js"></script>
<script type="text/javascript" src="framework/core/js/Fluid.js"></script>
<script type="text/javascript" src="framework/core/js/jquery.keyboard-a11y.js"></script>
<script type="text/javascript" src="framework/core/js/FluidDocument.js"></script>
<script type="text/javascript" src="framework/core/js/DataBinding.js"></script>
<script type="text/javascript" src="framework/core/js/FluidView.js"></script>
<script type="text/javascript" src="framework/core/js/FluidIoC.js"></script>
<script type="text/javascript" src="components/tooltip/js/Tooltip.js"></script>
<script type="text/javascript" src="components/inlineEdit/js/InlineEdit.js"></script>
<script type="text/javascript" src="components/undo/js/Undo.js"></script>
