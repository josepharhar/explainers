# The `<listbox>` element

The `<listbox>` element is intended to be an implementation of the [ARIA listbox
pattern](https://www.w3.org/WAI/ARIA/apg/patterns/listbox/) and a replacement
for `<select multiple>` which is more stylable and customizable.

The `<listbox>` element is a form-associated element. Any `<option>` descendants
in the flat tree are selectable by the user and will be reflected in the
`<listbox>`'s value.

## Content model

Like the `<button>` element, the `<listbox>` element must not have any
descendants which are interactive content or have the `tabindex` attribute. The
HTML parser will implicitly end `<listbox>` tags when appending tags
representing interactive content. Appending interactive content from script will
emit console warnings if feasible.

Preventing interactive content from being appended to a `<listbox>` is
imperative for accessibility.

## Attributes

The following attributes are supported the same was as they are for `<select
multiple>` and all other form-associated elements:
* `disabled`
* `form`
* `name`
* `required`

### `multiple`

When the `multiple` attribute is present, multiple `<option>`s may be selected
at the same time.

## Pseudo-classes

### `:selected`

The selected `<option>` element gets the `:selected` pseudo-class applied to it.
If this `<listbox>` has the `multiple` attribute, then each selected `<option>`
will get the `:selected` pseudo-class.

## Keyboard interaction

`<listbox>` supports exactly what is specified for keyboard interaction in the
ARIA practices here:
https://www.w3.org/WAI/ARIA/apg/patterns/listbox/#keyboardinteraction

## ARIA roles

`<listbox>` support exactly what is specified in the ARIA practices here:
https://www.w3.org/WAI/ARIA/apg/patterns/listbox/#wai-ariaroles,states,andproperties

## IDL

The IDL of `<listbox>` is very similar to `<select>`.

```idl
interface HTMLListboxElement : HTMLElement {
  attribute boolean disabled;
  readonly attribute HTMLFormElement? form;
  attribute boolean multiple;
  attribute DOMString name;
  attribute boolean required;
  readonly attribute DOMString type;
  attribute DOMString value;
  readonly attribute HTMLOptionsCollection options;
  readonly attribute HTMLOptionscollection selectedOptions;

  readonly attribute boolean willValidate;
  readonly attribute ValidityState validity;
  readonly attribute DOMString validationMessage;
  boolean checkValidity();
  boolean reportValidity();
  undefined setCustomValidity(DOMString error);

  readonly attribute NodeList labels;
}
```

The following IDL attributes reflect their content attribute of the same name:
* `disabled`
* `multiple`
* `name`
* `required`

The `form` IDL attribute returns the `<listbox>`'s form owner.

The `type` IDL attribute returns `"listbox"`.

The `value` IDL attribute returns the value of the currently selected option. If
multiple options are selected, then the value of the first selected option is
returned.

> **_NOTE:_** `<select multiple>` just returns the first option's value.
> Wouldn't it be better to return the values of all selected options
> concatenated together with spaces between them?
 
The `options` IDL attribute returns an `HTMLOptionsCollection` containing all
descendant `<option>` elements in the flat tree.

The `selectedOptions` IDL attribute returns an `HTMLOptionsCollection`
containing all of the selected descendant `<option>` elements in the flat tree.

The following validity IDLs are supported the same way as they are for other
HTML form-associated elements:
* `willValidate`
* `validity`
* `validationMessage`
* `checkValidity()`
* `reportValidity()`
* `setCustomValidity()`

The `labels` IDL attribute returns a `NodeList` of all `<label>` elements whose
labeled control is this `<listbox>`.

## Typeahead

The `<listbox>` element supports typeahead, where the textContent of each option
is used to match against what the user has typed in.

> **_NOTE:_** The angular cdk listbox supports an attribute to specify unique
> values for typeahead. Should we do the same?
> https://material.angular.io/cdk/listbox/overview#option-typeahead

## User-agent styles

The `<listbox>` element will have a set of default styles supplied by the
user-agent. The actual styles are TBD.
