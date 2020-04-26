# Vuetify-Form-Base

Imagine you get this data as JS-Object and you have to create an editable form.

```javascript
Model: {
	name: 'Stoner',
	position: 'Admin',
	tasks: [
		{ 
		  done: true,
		  title: 'make refactoring' 
		},
		{ 
		  done: false,
		  title: 'write documentation'  
		},
		{ 
		  done: true,
		  title: 'remove logs'  
		}        
	]        
}
```

Normally you have to flatten the Data-Structure and map all to an appropriate Format. Then you have to define a HTML-Form and animate it with your Data. 

With **Vuetify-Form-Base** create a Schema Object with the same Structure as your Data.

```javascript
Schema: {
	name: { type:'text', label:'Name' },
	position: { type:'text', label:'Position' },
	tasks: { 
		type: 'array',
		schema: { 
			done:{ type:'checkbox', label:'done', flex:3}, 
			title:{ type:'text', flex:9 }
		} 
	}
}  
```

and you will get a working Form:

![Form](./images/array-schema.PNG)

If you have to generate Forms or you have to edit Data presented as JSON- or JS-Objects, then take a closer look at **Vuetify-Form-Base** and try it. It can make your work much easier and save your time. This Form Generator works as [Vue.js 2.0 Component](https://vuejs.org/) and can simplify your Work by automatically creating Forms, based on your Schema-Definition. 

Furthermore if you don't define a Schema, then **Vuetify-Form-Base** tries to generate a schema automatically. This works if the Data Values are of Type 'string', 'number' or 'bool'.

**Vuetify-Form-Base** uses the well known and excellent [Component Framework Vuetify](https://vuetifyjs.com/) to style and layout your Form. Vuetify Controls have a clear, minimalistic design and support responsive Design.


---
## Demo

[Here you can see a Demo with Key-Examples](https://wotamann.github.io/)

or

Clone or download this Project, change current directory to **./vuetify-form-base/example**  and then run

`npm install`

`npm run serve`

---
## Intro

**vuetify-form-base** is a [Vue Component](https://vuejs.org/v2/guide/components.html) and can easily integrated into any Vue Project.   

```HTML
<v-form-base :model="myModel" :schema="mySchema" @input="handleInput" />
<!-- is ident with  -->
<v-form-base :value="myModel" :schema="mySchema" @input="handleInput" />
````

The Schema-Object has the **same Structure** as the Model-Object. Create a Schema by copying the Model-Object and replace the Values of the Model-Object by Definitions for your your Schema. This corresponding Schema-Object defines type, layout and functional behaviour of the Controls in your Form. 

![Form Example](./images/dat-schema.PNG)

---

The [Component Framework Vuetify 2.0](https://vuetifyjs.com/) styles your Form. The Controls have a clear design, but don't worry if you need more you can change your style in a lot of ways. For more details see section **Style with CSS**

#### Autogenerating Schema
If you don't define a Schema, then **Vuetify-Form-Base** tries to generate a schema automatically. But this works only if the Model Values are of Type 'String','Number' or 'Bool'.

Based on an existing Model-Object **vuetify-form-base** generates a full editable Form. 
Layout and Functionality are defined in a Schema-Object, which has the same Property structure as the Model-Object. Your Data-Object keeps full reactive and any Input or Change in your Form triggers an Event too. If you have a deep nested Model-Object or an Array-Structure you can direct work on it. There is no need to flatten or modify your Data Presentation.


![Form Example](./images/formbase01.PNG)

Changing any Field in the Form gives you a **reactive Result** in your Model-Object. 
Furthermore you can **synchronize** two or more Forms by using same Model-Object. 

If you want a **Partial-Form** which displays only parts of your Data.Object, then link a property of your Data-Object to your **vuetify-form-base** Component. 

And if necessary you can also build a **Form in Form** by using **Slots**.

Use the **v-on directive** to listen to **Events** for 'Focus', 'Input',  'Click', 'Blur', 'Resize', 'Intersect', 'Mouse' and 'Swipe'. 'Change' will catch all Value changing Events like 'Input' and 'Click'. 'Watch' will listen to 'Focus', 'Input', 'Blur' and 'Click'. 'Update' will catch all Events. 

```HTML
<!-- No ID defined -->
<v-form-base 
  :model="myModel"
  :schema="mySchema"
  @input="handleInput"
  @resize="handleResizeEvent"
/>

<!-- ID defined  -->
<v-form-base 
  id="form-base-person"
  :model="myModel"
  :schema="mySchema"
  @input:form-base-person="handleInput"
  @resize="handleResizeEvent"
/>

````

### Supported Controls from **Vuetify UI Input & Controls**  
---
````javascript
  // Textfield - Text: 
  schema: { ctrl: 'text' }  // shorthand definition
  
  schema: { 
    ctrl: { type:'text', ...} 
  }
  // Textfield - Password: 
  schema: { ctrl: 'password' }
  
  schema: { 
    ctrl: { type:'password', ...} 
  }
  // Textfield - Email:  
  schema: { ctrl: 'email' }
  
  schema: { 
    ctrl: { type:'email', ...} 
  }
  // Textfield - Number:  
  schema: { ctrl: 'number' }
	
  schema: { 
    ctrl: { type:'number', ...} 
  }

  // Attributes from 
  schema: { 
    ctrl: { type:'text', label:'Search', hint:'Books', prependIcon:'search', clearable } 
  }
````

  [More Informations to Vuetify-Textfield Attributes find here](https://vuetifyjs.com/en/components/text-fields/). 

---
#### Native Type of HTML-INPUT
Prop 'ext' in combination with Type:'text' make the native [HTML Input Type ]( https://www.w3schools.com/tags/att_input_type.asp ) accessable. 

````javascript
  mySchema:{    
    range:{ 
      type:'text', 
      ext:'range' 
    },
    color:{ 
      type:'text', 
      ext:'color',
      prependIcon: 'palette', 
      label:'Color'
    },    
    date:{ 
      type:'text', 
      ext:'date', 
      locale:'en',
      prependIcon: 'event', 
      label:'Date'
    },
    time:{ 
      type:'text', 
      ext:'time', 
      format:'24h',
      prependIcon: 'timer', 
      label:'Time'
    }
  }

````
---

#### File-Input: 
````javascript
	schema: { ctrl: 'file', ... }
	schema: { ctrl: { type:'file', ...}, ... }
````
[More Informations to Vuetify File-Input find here](https://vuetifyjs.com/en/components/file-inputs/). 

---

#### Textarea:
````javascript
	schema: { ctrl: 'textarea', ... }
	schema: { ctrl: { type:'textarea', ...}, ... }
````
[More Informations to Vuetify Textarea find here](https://vuetifyjs.com/en/components/textarea/). 

---

#### Checkbox:
````javascript 
	schema: { ctrl: 'checkbox', ... }
	schema: { ctrl: { type:'checkbox', ...}, ... }

#### Radio: 
	schema: { ctrl: { type:'radio', ...}, ... }

#### Switch: 
	schema: { ctrl: 'switch', ... }
	schema: { ctrl: { type:'switch', ...}, ... }
````
[More Informations to Vuetify Selection-Controls find here](https://vuetifyjs.com/en/components/selection-controls/). 

---
````javascript
  // Slider: 
	schema: { ctrl: 'slider', ... }
	schema: { ctrl: { type:'slider', ...}, ... }
````
[More Informations to Vuetify Sliders find here](https://vuetifyjs.com/en/components/sliders/). 

````javascript
  // Icon: 
	schema: { ctrl: 'icon', ... }
	schema: { ctrl: { type:'icon', ...}, ... }
````
[More Informations to Vuetify Icons find here](https://vuetifyjs.com/en/components/icons/). 
````javascript
  // Image: 
	schema: { ctrl: 'icon', ... }
	schema: { ctrl: { type:'img', src:'...', ...}, ... }
````
[More Informations to Vuetify Icons find here](https://vuetifyjs.com/en/components/icons/)
````javascript
  // Button: 
	schema: { ctrl: 'btn', ... }
	schema: { ctrl: { type:'btn', ...}, ... }
````
[More Informations to Vuetify Buttons find here](https://vuetifyjs.com/en/components/buttons/). 

````javascript
  // Button Group: 
	schema: { ctrl: 'btn-toggle', ... }
	schema: { ctrl: { type:'btn-toggle', ...}, ... }
````
[More Informations to Vuetify Button Groups find here](https://vuetifyjs.com/en/components/button-groups/). 

---

**_Select Data from Array defined in Schema_**

````javascript
  // Select:
	schema: { ctrl: 'select', ... }
	schema: { ctrl: { type:'select', ...}, ... }
````
[More Informations to Vuetify Select find here](https://vuetifyjs.com/en/components/select/). 
````javascript
  // Combobox:
	schema: { ctrl: 'combobox', ... }
	schema: { ctrl: { type:'combobox', ...}, ... }
````
[More Informations to Vuetify Combobox find here](https://vuetifyjs.com/en/components/combobox/). 
````javascript
  // Autocomplete:
	schema: { ctrl: 'autocomplete', ... }
	schema: { ctrl: { type:'autocomplete', ...}, ... }
````
[More Informations to Vuetify Autocomplete find here](https://vuetifyjs.com/en/components/autocomplete/). 

---

**_Select or Edit Array in your Model_**
````javascript
  // List: Edit  
	schema: { ctrl: 'list', ... }
	schema: { ctrl: { type:'list', ...}, ... }
````
[More Informations to Vuetify List-Item-Groups find here](https://vuetifyjs.com/en/components/list-item-groups/). 
````javascript
  // Treeview: 
	schema: { ctrl: 'treeview', ... }
	schema: { ctrl: { type:'treeview', ...}, ... }
````
[More Informations to Vuetify Treeview find here](https://vuetifyjs.com/en/components/treeview/). 
````javascript
  // Array: 
  model:{
    ctrlArray:[
      { idx:1, ctrl:'A'},
      { idx:2, ctrl:'B'},
      { idx:3, ctrl:'C'}
    ]
  }
	schema: { 
    ctrlArray: { 
      type:'array',
      // optional define key for array removing 
      key:'idx' // or ['idx','ctrl']
      // define schema of your items in array
      schema: { ctrl: 'text' }
    }, 
	}
````
---
````javascript
  // Card Grouping
  model:{
    group:{
      a: 'A',
      b: 'B',
      c: 'C'
    }
  }
	schema: { 
    group: { 
      type:'card',
      schema: { a:'text', b:'text', c:'text' }
    }, 
	}
````

[See more under Section 'Group Controls'](https://wotamann.github.io/) 

---
````javascript
  // Color Picker: 
	schema: { ctrl: 'color', ... }
	schema: { ctrl: { type:'color', ...}, ... }
  
  // Color Menu
  color:{ 
    type:'text', 
    ext:'color',
    prependIcon: 'palette', 
    label:'Color'
  }    
````
[More Informations to Vuetify Color-Pickers find here](https://vuetifyjs.com/en/components/color-pickers/). 

````javascript
  // Date Picker: 
  schema: { ctrl: 'date', ... }
  schema: { ctrl: { type:'date', ...}, ... }
  
  // Date Menu
  date:{ 
    type:'text', 
    ext:'date', 
    locale:'en',
    prependIcon: 'event', 
    label:'Date'
  }
````	
[More Informations to Vuetify Date-Pickers find here](https://vuetifyjs.com/en/components/date-pickers/). 

````javascript
  // Time Picker: 
  schema: { ctrl: 'time', ... }
  schema: { ctrl: { type:'time', ...}, ... }
  
  // Time Menu
  time:{ 
    type:'text', 
    ext:'time', 
    format:'24h',
    prependIcon: 'timer', 
    label:'Time'
  }

````
[More Informations to Vuetify Time-Pickers find here](https://vuetifyjs.com/en/components/time-pickers/). 
	
[See Example under Section 'Pickers'](https://wotamann.github.io/) 

---
## Installation

For proper working you need a Vue.js Project with Vuetify 2.0 installed. For more Details see [Vuetify 2.0 Quickstart](https://dev.vuetifyjs.com/en-US/getting-started/quick-start).  
After a successful installation of a Vue 2.6 Project with Vuetify 2.0  

    npm install vuetify-form-base --save

**vuetify-form-base** is a [Vue.js single-file component](https://vuejs.org/v2/guide/single-file-components.html) with a .vue extension and you can use it like any Vue-Component. 

In order for your application to work properly, you must wrap it in a [v-app](https://next.vuetifyjs.com/en-US/framework/default-markup) component. This component is required and can exist anywhere inside the body, but must be the parent of ALL Vuetify components. **v-content** needs to be a direct descendant of **v-app**. 

### Quickstart with VUE-File
```HTML
<!-- exampleFile.vue -->

<template>
  <v-app>
    <v-content>
      <v-container fluid>
        <v-form>
          <v-form-base :value="myModel" :schema="mySchema" @input="handleInput"/>
        </v-form>
      </v-container>   
    </v-content>
  </v-app>
</template>
```
```javascript
import VFormBase from 'vuetify-form-base';  

export default {	
  components:{ VFormBase },
  data () {
    return {
      myModel: {
        name: 'Jumo',
        password: '123456',
        email: 'base@mail.com',
        checkbox: true,
        select: 'Jobs',
      },   
      mySchema: {
        name: { type: 'text', label: 'Name' },
        password: { type: 'password', label: 'Password' },
        email: { type: 'email', label: 'Email' },
        checkbox: { type: 'checkbox', label: 'Checkbox' },
        select: { type: 'select', label: 'Select', items: ['Tesla', 'Jobs', 'Taleb'] }
      }
    }
  },
  methods:{
    handleInput(val){
      console.log(val) 
    }
  }
}
```
and you will get a full editable Form based on your schema and filled with your Model-Object. 

![Basic Form](./images/formbase2.PNG)

>INFORMATION: 
>
>Properties in 'myValue' without corresponding Prop in 'mySchema', are ignored and keep untouched, but a initial warning will be logged to console

---
## Example displaying nested Data-Object
 

In Reality sometimes you will have deep nested objects or arrays, which should be edited. **vuetify-form-base** works for you and flatten internally this nested object and build a plain Form.   

```javascript
      myValue: {
        name: 'Base',
        controls:{
          selection:{
            select: 'Tesla',
            selectM: ['Jobs'],
          },
          switch: [ true,false ],
          checkbox: [ false, true, { 
            checkboxArray: [ true, false ]}
          ]
        }       
      },

      mySchema: {
        name: { type: 'text', label: 'Name'},
        controls:{
          selection:{
            select: { type: 'select', label: 'Select', items: ['Tesla', 'Jobs', 'Taleb'] },        
            selectM: { type: 'select', label: 'M-Select', multiple:true, items: ['Tesla', 'Jobs', 'Taleb']}
          },
          switch: [ 
            { type: 'switch', label: '1' }, 
            { type: 'switch', label: '2' } 
          ],
          checkbox: [
            { type: 'checkbox', label: 'A' },
            { type: 'checkbox', label: 'B' }, 
            { checkboxArray: [
              { type: 'checkbox', label: 'C-A', color:'red' },
              { type: 'checkbox', label: 'C-B', color:'red' }
            ]}  
          ],
        }
      }
```

![Form Example](./images/deep.png)


---
## Example editing Data-Arrays
 
For editing arrays use the type 'array' and define an nested 'schema' property. 

```javascript
    mySchema: {
      tasks: {
        type: 'array',
        schema: { 
          done: { type: 'checkbox'  }, 
          title: { type: 'text' }
        }
      }  
    }
```

#### Type Array - Schema object

```javascript
    myValue: {      
      tasks: [
        {
          idx:0,
          done: true,
          title: 'make refactoring'
        },
        {
          idx:1,
          done: true,
          title: 'write documentation'
        },
        {
          idx:2,
          done: true,
          title: 'remove logs'
        }
      ]
    },
    mySchema: {
      tasks: {
        type: 'array',
        // optional for working on array (ie removing) define a key
        // IMPORTANT: don't use an editable key (because of permanent re-iteration on change) 
        key:'idx',
        schema: { 
          done: { type: 'checkbox', label: 'Ok', flex: 3 }, 
          title: { type: 'text', flex: 8 },            
        }
      }
    }
```

![Form Example](./images/array-template.png)

---
## Computed Schema
 
IF you want Schema Properties to be changed dynamic, then you must make your Schema Object a computed property. This Example turns the Radio Layout from Column to Row on Resizing to medium Size or greater. 

```javascript
    data () {
      return {
    
        myValue: {
          radio: 'A',
        }
    
      }   
    },
    computed: {          
    
      mySchema(){ 
        return {
          radio: { type: 'radio', row: this.row, options:['A','B'] }
        }
      },
    
      row () {
        return this.$vuetify.breakpoint.mdAndUp 
      }
    },
```
---

## Vuetify Display, Typography and Spacing

Integrate Vuetify-Display and Layout behaviour by using the Schema-Property 'class':

```javascript
    mySchema: {
      name: { type: 'text', class:'title d-flex d-sm-none ml-4 pa-1 float-left' },
    }
```
[More Info at Vuetify Display:](https://vuetifyjs.com/en/styles/display) 

[More Info at Vuetify Typography:](https://vuetifyjs.com/en/styles/typography) 

[More Info at Vuetify Spacing:](https://vuetifyjs.com/en/styles/spacing) 

[More Info at Vuetify Float:](https://vuetifyjs.com/en/styles/float) 


[See Example under Section 'Display, Typographie and Layout'](https://wotamann.github.io/) 

---

## Vuetify Grid

Integrate Vuetify-Grid behaviour by setting the Form-Base Property 'flex':

```html
  <form-base :flex="{ xs:12, sm:8, md:6, lg:4 }" ... />
  
  <!-- or shorthand xs:12  -->
  <form-base :flex="12" ... />
```

**Schema-Definition overrules Form-Base Definition!**

Get individual Grid-Control by using Schema-Properties 'flex', 'offset' and 'order'.

```javascript
    mySchema: {
      name1: { type: 'text', flex: { xs:12, sm:6, md:4 } },
      
      name2: { type: 'text', flex: 4, offset: 2, order: 1 },
      // flex: 4     // shorthand for flex: { xs:4 }
      // offset: 2   // shorthand for offset: { xs:2 }
      // order: 1    // shorthand for order: { xs:1 }
    }
```
---
    
A more responsive Solution with 'flex', 'offset' or 'order' needs an Object as Value. For more Details see Vuetify Documentation:  

[More Info at Vuetify Grid:](https://vuetifyjs.com/en/framework/grid#usage) 

[More Info at Vuetify Offset:](https://vuetifyjs.com/en/framework/grid#offset) 

[More Info at Vuetify Order:](https://vuetifyjs.com/en/framework/grid#order) 

---

## Link & Synchronize

Forms can be **linked** together using the same Model-Object. Changes in one Form are synchronized and reflected in the other Form. 

```HTML
	<v-form-base :model="myValue" :schema="mySchema" />
  <!-- is ident to  -->
	<v-form-base :value="myValue" :schema="mySchema" />

	<v-form-base id="form-sync" :model="myValue" :schema="mySchema" />
```
---

## Vuetify Controls API-Props

[Vuetify Controls have a API with Props](https://vuetifyjs.com/en/components/text-fields#api) These Props in Vuetify-Controls comes in **kebab-case** amd must for use in Schema-Object converted to **camelCase**

    <!-- vuetifyjs.com -->
    Input & Controls
      Text-fields
        API-Props   
          append-icon
          background-color 

```javascript
  mySchema: { 
    name: { type:'text', appendIcon:'menu', backgroundColor:'red' }  
  }
```
---

## Schema

```HTML
<v-form-base :schema="mySchema" ... />

<v-form-base 
  id="myId" 
  :model="myValue" 
  :schema="mySchema" 
  :flex="12" 
  :change:myId="myEventHandler"
/>
```
	
Schema is an Object, which defines and controls the behavior of your Form. Each Key in your Schema-Object should reflect a Key from your Data-Object. A minimalistic Definition of a Text-Input could look like this:

```javascript
data () {
  return {
    myValue:{
      name: 'Base'  
    }, 
    mySchema:{
      name: { type:'text'}  
    }
  }
}
```

The next example shows a more complex Schema:
  
```javascript  
    // Partials Functions for Rules
    const minLen = l => v => (v && v.length >= l) || `min. ${l} Characters`
    const maxLen = l => v => (v && v.length <= l) || `max. ${l} Characters`
    const required = msg => v => !!v || msg
    const validEmail: msg => v => /.+@.+\..+/.test(v) || msg
  
	  // Destruct value from obj and return a modified value! 
    const toUpper = ( {value} ) => typeof value === 'string' ? value.toUpperCase() : value 

    export default {
    
      components: { VFormBase },

      data () {
        return {
          // model
          myModel: {
            name: 'Base',
            password: '123456',
            email: 'base@mail.com'
          },
          // schema
          mySchema: {
            name: { 
              type: 'text', 
              label: 'Name', 
              hint:'Converts to UpperCase'
              toCtrl: toUpper, 
              fromCtrl:toUpper,
              rules: [ required('Name is required<>) ] 
              flex: 12, 
            },
            password: { 
              type: 'password', 
              label: 'Password', 
              hint:'Between 6-12 Chars', 
              appendIcon: 'visibility', 
              counter: 12, 
              rules: [ minLen(6), maxLen(12) ], 
              clearable: true, 
              flex: 12 
            },
            email: { 
              type: 'email', 
              label: 'Email', 
              rules: [ validEmail('No valid Email'), required('Email is required<>) ], 
              flex: 12 
            }
          }
        }
      }

    }
```

**Available Properties in Schema **
  
[For more Schema-Properties see Vuetify Controls API](https://vuetifyjs.com/en/components/text-fields#api)  

	schema:{
      
      type: string            // text, password, email, file, textarea 
                              // radio, switch, checkbox, slider,
                              // select, combobox, autocomplete, 
                              // array, list, treeview
                              // icon, btn, btn-toggle 
                              // date, time, color    

      sort: num               // use simple order to display items 

      order: num or object    // use Vuetify-Grid to order items responsive 
      flex:  num or object    // See Vuetify Grid
      offset: num or object   // See Vuetify Grid

      label string,           // label of item    
      placeholder: string,    // placeholder 
      hint: string,           // additional Info  
      tooltip: string | bool  // show tooltip - use Slots for individual text

      color: string
      backgroundColor:string
      class: string,            // inject classnames - schema:{ name:{ css:'small'}, ...  }
        
      mask: string,           // regex to control input  

      multiple: bool,         // used by type: select, combobox, autocomplete    
      required: bool,         // need an input value
      hidden: bool,           // hide item - set from another item
      disabled: bool,         
      readonly: bool,          
            
      appendIcon: icon        // click triggers event with icon-location
      prependIcon: icon       // click triggers event with icon-location

      items: array            // ['A','B'] used by type: select, combobox, autocomplete   
      options: array,         // ['A','B'] used by type:radio
      rules: array of Fn      // [ value => true || false, ... ]
      
      // must return a (modified) value!!
      toCtrl: function,       // ( {value, obj, data, schema} ) => value	
      fromCtrl: function,     // ( {value, obj, data, schema} ) => value
    }


## Events

We can use the v-on directive to listen to vuetify-form-base events **'focus', 'input', 'click', 'blur', 'change', 'watch', 'mouse', 'display', 'intersect', 'resize', 'swipe', 'update'** and run some Code when they’re triggered.

This Example use the Default ID and listen all events with 'update':

```HTML
    <!-- HTML -->
    <v-form-base :value= "myValue" :schema= "mySchema" @update= "update" />
```

The next Code has the Custom ID **'form-base-simple'**. In this case your v-on Directive must append the Custom ID like **@update:form-base-simple:**

```HTML
    <!-- HTML -->
    <v-form-base 
      id = "form-base-simple" 
      :value= "myValue" 
      :schema= "mySchema" 
      @update:form-base-simple= "update" 
    />
```

You can listen to one or more Events

```HTML
  <!-- HTML -->
  <!-- compose Listener to one or more of following Events: -->
  <v-form-base 
    :value= "myValue" 
    :schema= "mySchema" 
    
    @click= "log"
    @input= "log"
    @change="log"    // input|click
    @watch= "log"    // focus|input|click|blur
    @focus= "log"
    @blur=  "log"        
    @mouse= "log"    // mouseenter|mouseleave  
    @display= "log"  // resize|swipe|intersect 
    @intersect="log" // intersect - https://vuetifyjs.com/en/directives/intersect
    @resize= "log"
    @swipe=  "log"   // touch events        
    @update= "log"   // catch all events    
  />      
```

**The Event-Signature:**

```javascript
    change( {  on, id, key, value, params, obj, data, schema, parent, index, event } ){
      // destructure the signature object 
    }
```

    on -        Trigger Name  // focus|input|blur|click|resize|swipe|update 
    id -        Formbase-ID
    key -       key of triggering Element
    value -     value of triggering Element
    obj -       triggering Element { key, value, schema } 
    event -     the native trigger-event if available 
    params -    params object if available { text, x, y, tag, model, open, index }    
    index -     index of array of schemas  
    data -      Data-Object
    schema -    Schema-Object
    parent -    Formbase-Object - if available 
---
**Example: Use 'Change' Event to change Visibility on Password Element**

```HTML
    <!-- HTML -->
    <v-form-base :value="myValue" :schema="mySchema" @change="change">
```

```javascript
    ...

    mySchema: {
      firstPassword:{ type:'password', appendIcon:'visibility', .... }
    }
    
    ...
    
    change ({ on, key, obj, params }) {
      // test event is 'click' and comes from appendIcon on key 'firstPassword'
      if (on == 'click' && key == 'firstPassword' && (params && params.tag) == 'append') {         
        // toggle icon
        obj.schema.appendIcon = obj.schema.type === 'password'? 'lock': 'visibility'
        // toggle visibility 
        obj.schema.type = obj.schema.type === 'password'? 'text': 'password'
      }
    }
```
---
## Slots

Use Slots to pass Header and Footer into a Control. If necessary replace Controls by Slots. Any slot could be a v-form-base component itself.   
 
 ```HTML
    <v-form-base :value="myValue" :schema="mySchema" @update="update">

      <h4 slot="slot-top-key-name">Top Slot on Key Name</h4>
      <h4 slot="slot-top-type-radio">Top Slot on Types Radio</h4>
      
      <h4 slot="slot-item-key-password">Slot replaces Key Password</h4>
      
      <h4 slot="slot-bottom-key-name">Bottom Slot Key Name</h4>
      <h4 slot="slot-bottom-type-radio">Bottom Slot on Types Radio</h4>
      
      // Tooltip see css.vue in Example 
      <div slot="slot-tooltip" slot-scope="slotProps">
        {{ slotProps.obj.schema.tooltip }} has value '{{ slotProps.obj.value }}
      </div>
    
    </v-form-base>
```

[Try CSS & Slots in Example](https://wotamann.github.io/)

![Slots in Blue](./images/slot.png)

---
## [Form Validation](https://wotamann.github.io/)

If you need Form Validation you have to wrap **v-form-base** with **[v-form](https://next.vuetifyjs.com/en/components/forms#api)** and take the reference of v-form for working on.
    
```HTML    
    <!-- HTML -->    
    <v-form ref="form" v-model= "formValid" lazy-validation>
      <v-form-base :value= "myValue" :schema= "mySchema" @update= "update"/>
    </v-form>
```
```javascript
    <!-- JS -->
    validate () {
      this.$refs.form.validate()
    },

    resetValidation () {
      this.$refs.form.resetValidation()
    },
```
---

## Style with CSS 


Customize your **vuetify-form-base** component using CSS-Classnames 
 
>  IMPORTANT:  
>  Don't use `<style scoped>` in parents component, because scoped definitions
>  are inside the child component not accessable
   
### Formbase - ID

`#form-base` is the default ID of your component. If you need different CSS for two or more forms in the same parent component, then change default value by setting a different ID for each component and use this new ID. Using a 'custom-id' you have to modify the event-binding to @update:custom-id = "update" 


```CSS
    <!-- Default ID CSS-Style -->   	
    #form-base {...} 
```
```HTML
    <!-- HTML-Template -->   
    <v-form-base @update= "update" />  
```

```CSS 
    <!-- Custom-ID CSS-Style -->   	
    #custom-id {...} 
```
```HTML

    <!-- HTML-Template -->   
    <v-form-base id="custom-id" @update:custom-id= "update" />  
```

---

### General - Classname

    #form-base  {...}              

### Type - Classnames

  
  Style all items of a specific type, then use type specific classnames. They start with `type-` appended by any `type`. You can use following types in your Schema-Object: 

`'text', 'email', 'password', 'textarea', 'select', 'autocomplete', 'combobox', 'radio', 'checkbox', 'slider', 'switch', 'date', 'time'` 
	  
    #form-base .type-text { color: #44A }}           	  
    #form-base .type-email { font-weight:500; }  

### Key - Classnames

  Set Classname of deep key in your Data-Object, by converting **.dot notation** 'person.adress.city' into **kebab case** 'person-adress-city' prepending 'key-' 

    <!-- 
	    myValue{ person:{ adress:{ city:'',... } ... } ... } 
      CSS Classname to access to key 'city'
    -->
    #form-base .key-person-adress-city { font-weight:500; }    
    

    <!-- 
      Access to myValue: { name:'' }
      CSS Classname to access key 'name' 	       
    -->
    #form-base .key-name { font-weight:500; }            
    
    <!-- 
      myValue: { controls: { slide: [25, 64]  } 
      Access First Entry in Array of Key Slide 
    -->
    #form-base .key-controls-slide-0 { font-weight:500; }  


### Validate with Pseudoselectors
	  
    #form-base .item input:valid { background-color: #afa; }
    #form-base .type-email input:invalid { background-color: #faa; }
    #form-base .key-name input:focus { background-color: #ffd; }   

### CSS - Example
    <!-- JS -->
    myValue: {
        name: 'Base',
        password: '123456',
        email: 'base@mail.com',
        controls: {
          checkbox: true,
          switch: true,
          slider: 33,
          radioA: 'A',
          radioB: 'B'
        }
      }

     <!-- CSS  -->
    <style>
      #form-base { 
        border: 1px solid #cb2; 
        background-color: #ffe; 
        padding:2rem 
      }
      
      /* CSS Item --- set all items  */
      #form-base .item { 
        border-left: 1px dashed #29D; 
        border-top: 1px dashed #29D; 
        padding:1rem 
      }

      /* CSS Type --- set all items with type */
      #form-base .type-switch { border-bottom: 3px solid #E23}
      #form-base .type-checkbox { background-color: #fdd }

      /* CSS Keys --- select key in object 'myValue.controls.slider' */
      #form-base .key-controls-slider { background-color: #fec }
    </style>

[Try CSS & Slots in Example](https://wotamann.github.io/)

![Slots in Blue](./images/css.PNG)

---
## Features

* Vue-Component
* integrates UI framework Vuetify with responsive Layout and Support of Grid
* Use a lot of Vuetify Control & Input types inclusive most of available API-Props
* Get full configurable Forms based on Schema Definition
* Edit plain or deep nested objects including Arrays, without the need to flatten your data
* Get a full, reactive Result
* Listen on 'Resize', 'Focus', 'Input', 'Blur', 'Click', 'Swipe', 'Mouse' and 'Update' Events
* Use Slots to pass Header and Footer into a Control or replace a Control by a Slot.  Use  Slots to individualize your Tooltip   
* Configurable CSS Style 


---

#### Version 0.1.17
- fixed known  problem of splicing arrays in v-for and index key   

#### Version 0.1.11
- added support for grouping some control  | { type:'card', ...}   

#### Version 0.1.9
- added support for v-img | { type:'img'}   

#### Version 0.1.8
- Revision of example, 
- bug fixed with tooltip in array   

#### Version 0.1.8
- tooltip added

#### Version 0.1.6
- tooltip added

#### Version 0.1.5
- Event 'blur' available  

#### Version 0.1.4

- File Input added (type:'file')
- Pickers for Color, Date and Time added/adapted (type:'color|date|time')   

#### Version 0.1.3

- control type 'list' and 'array' added

---
## Dependencies

vue >= 2.6

vuetify >= 2.0

lodash > 4.15

vue-the-mask

---
## Similar Projects


[vue-form-generator](https://github.com/icebob/vue-form-generator)

[vue-formular](https://github.com/matfish2/vue-formular)

---
## License

**vuetify-form-base** is available under the MIT license.
