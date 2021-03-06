---
id: native methods
title: native methods
sidebar_label: native methods
---

## Introduction

Following native methods have been implemented:
- scrollTo
- measure

## measure

### Arguments

animatedRef

### Returns

Object which contains following fields
- x 
- y 
- width 
- height 
- pageX 
- pageY 

### Example

```js
const Comp = () => {
  const aref = useAnimatedRef();

  useDerivedValue(() => {
    const measured = measure(aref);
    // ...
  })

  return <View ref={aref} />;
};
```

## scrollTo

### Arguments

animatedRef

### Returns

void

### Example

```js
const Comp = () => {
  const aref = useAnimatedRef()
  const scroll = useSharedValue(0)

  useDerivedValue(() => {
    scrollTo(aref, 0, scroll.value * 100, true);
  });

  const items = Array.from(Array(10).keys());

  return (
    <View>
      <Button title="scroll down" onPress={ () => {
        scroll.value = scroll.value + 1
        if (scroll.value >= 10) scroll.value = 0
      } } />
      <View  style={ { width: 120, height: 200, backgroundColor: 'green', } }>
        <ScrollView ref={ aref } style={ { backgroundColor: 'orange', width: 120 } }>
          { items.map((_, i) => (<View key={ i } style={ { backgroundColor: 'white', width: 100, height: 100, margin: 10 } } />)) }
        </ScrollView>
      </View>
    </View>
  )
}
```