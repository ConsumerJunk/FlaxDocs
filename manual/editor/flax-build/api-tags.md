# API tags

## API_CLASS(...)

Use it on class to expose it to the scripting API. You can specify custom attributes in the braces.
Example:

```cpp
/// <summary>
/// Actor that links to the animated model skeleton node transformation.
/// </summary>
API_CLASS(sealed) class BoneSocket : public Actor
{
...
}
```

## API_PROPERTY(...)

Use it on the property getter/setter methods to expose property to the scripting API. You can specify custom attributes in the braces.
Example:

```cpp
/// <summary>
/// Gets the value indicating whenever use the target node scale. Otherwise won't override the actor scale.
/// </summary>
/// <returns>If set to <c>true</c> the node socket will use target node scale, otherwise it will be ignored.</returns>
API_PROPERTY()
FORCE_INLINE bool GetUseScale() const
{
    return _useScale;
}

/// <summary>
/// Sets the value indicating whenever use the target node scale. Otherwise won't override the actor scale.
/// </summary>
/// <param name="value">If set to <c>true</c> the node socket will use target node scale, otherwise it will be ignored.</param>
API_PROPERTY()
void SetUseScale(bool value);
```

## API_FUNCTION(...)

Use it on the function to expose property to the scripting API. You can specify custom attributes in the braces.
Example:

```cpp
/// <summary>
/// Updates the actor transformation based on a skeleton node.
/// </summary>
API_FUNCTION()
void UpdateTransformation();
```

## API_PARAM(...)

Use it on the function parameters to adjust the parameter convertion between scripting and native.
Example:

```cpp
API_FUNCTION()
int32 CalculateSpeedParams(API_PARAM(ref) Vector3& offset);
```

## Tag parameters

Tag attributes tha can be added to the API tags braces to edjust the bindigns logic:

* `Static` - marks the method/class/property to not use instance of the object but be static in code
* `Sealed` - makes the class to be final and blocks inheritance
* `Abstract` - makes the class to be abstract (cannot create object of it, can be only inherited)
* `Public`/`Protected`/`Private` - access levels specified for methods/classes/properties to define the visibility in the scritping API
* `InBuild` - marks type (class, struct, enum) as in-build into scripting API (skips generation by assuming it's already in the bindings API)
* `Attributes="..."` - adds a custom attributes to the generated type or member that are added to C# types attributes
* `ReadOnly` - makes the field in class as read-only (only getter will be generated, no setter)
* `NoProxy` - skips proxy method generation (for methods)
* `NoConstructor` - skips class constructor method generation
* `Ref` - marks the function parameter to be passed by reference
* `NoPod` - marks the structure as non-POD type by force (bindings generator will use wrapper structure by force and structure won't be passed by native value in bindings glue code)
* `Name="..."` - overrides the name of the type to be used in the bindings
* `Namespace="..."` - overrides the namespace of the type to be used in the bindings

## Special cases

### Array&lt;T&gt;

If property or method uses native Array&lt;T&gt; as input or output it will be interpreted as T[] in scripting.
Also, the bindings generator will implement atomatic convertion between native and managed object type (including copy operation).
If you want to return an array of items from native method you can return it by value (eg. `API_FUNCTION() Array<Guid> GetIds()`). Bindings generator will convert it into managed array (supported types for array elements are value types, enums, strings and scripting objects such as actors, scripts, assets pointers, object references).

### Dictionary&lt;KeyType, ValueType&gt;

If property or method uses native Dictionary&lt;KeyType, ValueType&gt; as input or output it will be interpreted as System.Collections.Generic.Dictionary&lt;KeyType, ValueType&gt; in scripting.
Also, the bindings generator will implement atomatic convertion between native and managed object type (including copy operation).