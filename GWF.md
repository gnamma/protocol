# Gnamma World File (GWF)

A GWF is a file which is used to describe a world's environment to a Gnamma client. It is *not* used for configuration of the server, and is *not* used for interactions of elements.

The file format is an XML derivative. The design of GWF is currently very ambiguous, and thus, this file is going to be used to do some mockups of what things *could* look like.

## 13th September 2016 - HTMLish

```xml
<room>
    <el name="ground" model="box" scale-x="5" scale-z="5" x="0" y="-1" z="0"/>

    <group name="items" scale-x="0.5" scale-y="22">
        <el name="glass" model="glass.fbx"/>

        <box scale-x="22" scale-y="33"/>
    </group>
</room>
```

- Primitives have their own tags (`<box>`, `<plane>`, `<sphere>`, `<cylinder>`)
- Non primitives are supplied through an `<el>` tag with a `model` attribute
- Scale is provided through the `scale-x`, `scale-y` and `scale-z` attributes
- Position is provided through the `x`, `y` and `z` attributes
- Elements (no matter if they are primitive or non primitive) can be put into a group in the `<group>` tag
  - In a group, scale compounds (Absolute scale of a box with scale `0.5` inside a group with scale `3` is `1.5`

## 18th September 2016 - HTML + Sugar

```xml
<room>
    <plane name="ground">
        <box each-corner sit name="corner_{{side}}" scale-y="5"/>
    </plane>
</room>
```

- Same sort of basic XML layout as the previous iteration
- In order to make construction of composite/complex objects easier should provide a lot of syntactic sugar.
  - `each-corner` puts one of the element in each corner of the parent
  - `sit` ensures that the bottom of the element is touching the top of its parent
  - Can use little templating variables like `{{side}}` and `{{parent.name}}` to better customise the values of the object.
