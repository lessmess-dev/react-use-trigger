# react-use-trigger

[![Build Status](https://travis-ci.org/ilyalesik/react-use-trigger.svg?branch=master)](https://travis-ci.org/ilyalesik/react-use-trigger)
[![npm version](https://img.shields.io/npm/v/react-use-trigger.svg)](https://www.npmjs.com/package/react-use-trigger)

React Hook for trigger effect from any place of code. It is an implementation a Pub-Sub strategy on React Hooks. 

```javascript
import {createTrigger, useTriggerEffect} from "react-use-trigger";

const fooTrigger = createTrigger();

export const Subscriber = () => {  
    useTriggerEffect(() => {
        // make some effect
    }, fooTrigger);
  
    return <div />;
}

export const Sender = () => { 
    return <button onClick={() => {
        fooTrigger() // call trigger
    }}>Send</button>
}
```

Also, `useTrigger` may be used for combine with other inputs:
```javascript
export const Subscriber = (props) => {  
    const fooTriggerValue = useTrigger(fooTrigger);
    const [someState, setSomeState] = useState();
    
    useEffect(() => {
        // make some effect
    }, [fooTriggerValue, props.someProp, someState]);
  
    return <div />;
}
```

## Installation

Install it with yarn:

```
yarn add react-use-trigger
```

Or with npm:

```
npm i react-use-trigger --save
``` 

## API

#### `createTrigger(): TriggerWrapper;`
Create a trigger.
`TriggerWrapper` is function, that update value of trigger. 


#### `useTrigger(triggerWrapper: TriggerWrapper): string;`

Returns current value of trigger. A string, generated by [nanoid](https://github.com/ai/nanoid).

Can be used for combine trigger with other inputs:
```javascript
export const Subscriber = (props) => {  
    const fooTriggerValue = useTrigger(fooTrigger);
    const [someState, setSomeState] = useState();
    
    useEffect(() => {
        // make some effect
    }, [fooTriggerValue, props.someProp, someState]);
  
    return <div />;
}
```

#### `useTriggerEffect(create: () => MaybeCleanUpFn, triggerWrapper: TriggerWrapper): void;`

Call effect (from `create`) for every change of trigger.
