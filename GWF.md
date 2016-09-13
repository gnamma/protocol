# Gnamma World File (GWF)

A GWF is a file which is used to describe a world's environment to a Gnamma client. It is *not* used for configuration of the server, and is *not* used for interactions of elements.

The file format is an XML derivative. The design of GWF is currently very ambiguous, and thus, this file is going to be used to do some mockups of what things *could* look like.

## 13 September 2016

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
