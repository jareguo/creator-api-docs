## `EventTarget` Class


Defined in: [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:99](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L99)

Module: [cc](../modules/cc.md)


EventTarget is an object to which an event is dispatched when something has occurred.
Entity are the most common event targets, but other objects can be event targets too.

Event targets are an important part of the Fireball event model.
The event target serves as the focal point for how events flow through the scene graph.
When an event such as a mouse click or a keypress occurs, Fireball dispatches an event object
into the event flow from the root of the hierarchy. The event object then makes its way through
the scene graph until it reaches the event target, at which point it begins its return trip through
the scene graph. This round-trip journey to the event target is conceptually divided into three phases:
- The capture phase comprises the journey from the root to the last node before the event target's node
- The target phase comprises only the event target node
- The bubbling phase comprises any subsequent nodes encountered on the return trip to the root of the tree
See also: http://www.w3.org/TR/DOM-Level-3-Events/#event-flow

Event targets can implement the following methods:
 - _getCapturingTargets
 - _getBubblingTargets


### Index



##### Methods

  - [`on`](#on) Register an callback of a specific event type on the EventTarget.
  - [`off`](#off) Removes the listeners previously registered with the same type, callback, target and or useCapture,
if only type is passed as parameter, all listeners registered with that type will be removed.
  - [`targetOff`](#targetoff) Removes all callbacks previously registered with the same target (passed as parameter).
This is not for removing all listeners in the current event target,
and this is not for removing all listeners the target parameter have registered.
It's only for removing all listeners (callback and target couple) registered on the current event target by the target parameter.
  - [`once`](#once) Register an callback of a specific event type on the EventTarget,
the callback will remove itself after the first time it is triggered.
  - [`dispatchEvent`](#dispatchevent) Dispatches an event into the event flow.
The event target is the EventTarget object upon which the dispatchEvent() method is called.
  - [`emit`](#emit) Send an event to this object directly, this method will not propagate the event to any other objects.
The event will be created from the supplied message, you can get the "detail" argument from event.detail.



### Details




<!-- Method Block -->
#### Methods


##### on

Register an callback of a specific event type on the EventTarget.

| meta | description |
|------|-------------|
| Returns | <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Function" class="crosslink external" target="_blank">Function</a> 
| Defined in | [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:217](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L217) |

###### Parameters
- `type` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String" class="crosslink external" target="_blank">String</a> A string representing the event type to listen for.
- `callback` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Function" class="crosslink external" target="_blank">Function</a> The callback that will be invoked when the event is dispatched.
                             The callback is ignored if it is a duplicate (the callbacks are unique).
	- `event` <a href="../classes/Event.html" class="crosslink">Event</a> event
- `target` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object" class="crosslink external" target="_blank">Object</a> The target (this object) to invoke the callback, can be null
- `useCapture` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Boolean" class="crosslink external" target="_blank">Boolean</a> When set to true, the capture argument prevents callback
                             from being invoked when the event's eventPhase attribute value is BUBBLING_PHASE.
                             When false, callback will NOT be invoked when event's eventPhase attribute value is CAPTURING_PHASE.
                             Either way, callback will be invoked when event's eventPhase attribute value is AT_TARGET.

##### Examples

```js
node.on(cc.Node.EventType.TOUCH_END, function (event) {
    cc.log("this is callback");
}, node);
```

##### off

Removes the listeners previously registered with the same type, callback, target and or useCapture,
if only type is passed as parameter, all listeners registered with that type will be removed.

| meta | description |
|------|-------------|
| Defined in | [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:274](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L274) |

###### Parameters
- `type` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String" class="crosslink external" target="_blank">String</a> A string representing the event type being removed.
- `callback` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Function" class="crosslink external" target="_blank">Function</a> The callback to remove.
- `target` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object" class="crosslink external" target="_blank">Object</a> The target (this object) to invoke the callback, if it's not given, only callback without target will be removed
- `useCapture` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Boolean" class="crosslink external" target="_blank">Boolean</a> Specifies whether the callback being removed was registered as a capturing callback or not.
                             If not specified, useCapture defaults to false. If a callback was registered twice,
                             one with capture and one without, each must be removed separately. Removal of a capturing callback
                             does not affect a non-capturing version of the same listener, and vice versa.

##### Examples

```js
// register touchEnd eventListener
var touchEnd = node.on(cc.Node.EventType.TOUCH_END, function (event) {
    cc.log("this is callback");
}, node);
// remove touch end event listener
node.off(cc.Node.EventType.TOUCH_END, touchEnd, node);
// remove all touch end event listeners
node.off(cc.Node.EventType.TOUCH_END);
```

##### targetOff

Removes all callbacks previously registered with the same target (passed as parameter).
This is not for removing all listeners in the current event target,
and this is not for removing all listeners the target parameter have registered.
It's only for removing all listeners (callback and target couple) registered on the current event target by the target parameter.

| meta | description |
|------|-------------|
| Defined in | [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:329](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L329) |

###### Parameters
- `target` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object" class="crosslink external" target="_blank">Object</a> The target to be searched for all related listeners


##### once

Register an callback of a specific event type on the EventTarget,
the callback will remove itself after the first time it is triggered.

| meta | description |
|------|-------------|
| Defined in | [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:351](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L351) |

###### Parameters
- `type` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String" class="crosslink external" target="_blank">String</a> A string representing the event type to listen for.
- `callback` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Function" class="crosslink external" target="_blank">Function</a> The callback that will be invoked when the event is dispatched.
                             The callback is ignored if it is a duplicate (the callbacks are unique).
	- `event` <a href="../classes/Event.html" class="crosslink">Event</a> event
- `target` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Object" class="crosslink external" target="_blank">Object</a> The target (this object) to invoke the callback, can be null
- `useCapture` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/Boolean" class="crosslink external" target="_blank">Boolean</a> When set to true, the capture argument prevents callback
                             from being invoked when the event's eventPhase attribute value is BUBBLING_PHASE.
                             When false, callback will NOT be invoked when event's eventPhase attribute value is CAPTURING_PHASE.
                             Either way, callback will be invoked when event's eventPhase attribute value is AT_TARGET.

##### Examples

```js
node.once(cc.Node.EventType.TOUCH_END, function (event) {
    cc.log("this is callback");
}, node);
```

##### dispatchEvent

Dispatches an event into the event flow.
The event target is the EventTarget object upon which the dispatchEvent() method is called.

| meta | description |
|------|-------------|
| Defined in | [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:396](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L396) |

###### Parameters
- `event` <a href="../classes/Event.html" class="crosslink">Event</a> The Event object that is dispatched into the event flow


##### emit

Send an event to this object directly, this method will not propagate the event to any other objects.
The event will be created from the supplied message, you can get the "detail" argument from event.detail.

| meta | description |
|------|-------------|
| Defined in | [https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js:410](https:/github.com/cocos-creator/engine/blob/master/cocos2d/core/event/event-target.js#L410) |

###### Parameters
- `message` <a href="https://developer.mozilla.org/en/JavaScript/Reference/Global_Objects/String" class="crosslink external" target="_blank">String</a> the message to send
- `detail` Any whatever argument the message needs



