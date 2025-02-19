# @blockly/field-colour-hsv-sliders [![Built on Blockly](https://tinyurl.com/built-on-blockly)](https://github.com/google/blockly)

A [Blockly](https://www.npmjs.com/package/blockly) colour field using HSV sliders for editing.

![A Blockly workspace showing the HSV sliders.](readme-media/hsv_sliders_screenshot.png)

## Installation

### Yarn
```
yarn add @blockly/field-colour-hsv-sliders
```

### npm
```
npm install @blockly/field-colour-hsv-sliders --save
```

## Usage
This plugin adds a field type `FieldColourHsvSliders` that is registered to the name `'field_colour_hsv_sliders'`. This field is an extension of the `Blockly.FieldColour` field and outputs values in the same hexadecimal string format `'#rrggbb'` even though the UI represents the colour in the HSV colour space. See the [Blockly.FieldColour documentation](https://developers.google.com/blockly/guides/create-custom-blocks/fields/built-in-fields/colour#creation) on what parameters and configurations this field supports, although unlike `Blockly.FieldColour`, this field does not use colour swatches and thus ignores options related to the swatches such as `'colourOptions'`.

To use it, you'll need to add this field to a block type definition, and add that block to your toolbox. See below for an example of defining a block type that uses this field.

### JSON

```js
import * as Blockly from 'blockly';
import '@blockly/field-slider';
Blockly.defineBlocksWithJsonArray([
  {
    'type': 'colour_hsv_sliders',
    'message0': 'hsv %1',
    'args0': [
      {
        'type': 'field_colour_hsv_sliders',
        'name': 'COLOUR',
        'colour': '#ff0000'
      }
    ],
    'output': 'Colour',
    'style': 'colour_blocks'
  }
]);
Blockly.JavaScript['colour_hsv_sliders'] = function(block) {
  const code = Blockly.JavaScript.quote_(block.getFieldValue('COLOUR'));
  return [code, Blockly.JavaScript.ORDER_ATOMIC];
};
```

### JavaScript

```js
import * as Blockly from 'blockly';
import {FieldColourHsvSliders} from '@blockly/field-colour-hsv-sliders';
Blockly.Blocks['colour_hsv_sliders'] = {
  init: function () {
    this.appendDummyInput()
      .appendField('hsv ')
      .appendField(new FieldColourHsvSliders('#ff0000'), 'COLOUR');
    this.setOutput(true, 'Colour');
    this.setStyle('colour_blocks');
  }
};
Blockly.JavaScript['colour_hsv_sliders'] = function(block) {
  const code = Blockly.JavaScript.quote_(block.getFieldValue('COLOUR'));
  return [code, Blockly.JavaScript.ORDER_ATOMIC];
};
```

## License

Apache 2.0
