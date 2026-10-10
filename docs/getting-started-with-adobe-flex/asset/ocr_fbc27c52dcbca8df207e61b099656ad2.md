![](bbox=[0.22, 0.16, 0.44, 0.35])

# Figure 6.3 - States View

+   4. Now add a TextArea to this new state and define some properties for the TextArea as shown below.

```
```
<mx:TextArea id="txt1" x="10" y="10" width="260" height="210"
 text="My First State" fontSize="20" textAlign="center"
 backgroundColor="#FFEA00"/>
```
```

+   5. You can add one more state in the same manner as shown earlier in Figure 6.3 and name it *secondState*. Add as many states as you would like. You can even add multiple components of your choice to each new state.

+   6. You can check the source view to see what happened behind the scenes while we created these new states and added components to them. Listing 6.1 shows you the code that is generated.

```
```
<mx:Panel id="panel1" x="0" y="0" width="300" height="300"
 layout="absolute" title="Learn how to change states">
 <mx:Button x="99" y="228" label="Change"
 click="onClick(event)"/>
</mx:Panel>
<mx:states>
 <mx:State name="firstState">
 <mx:AddChild relativeTo="[panel1]" position="lastChild">
 <mx:TextArea id="txt1" x="10" y="10" width="260"
 height="210"
 text="My First State" fontSize="20" textAlign="center"
 backgroundColor="#FFEA00"/>
 </mx:AddChild>
 </mx:State>
 <mx:State name="secondState">
 <mx:AddChild relativeTo="[panel1]" position="lastChild">
 <mx:TextArea id="txt2" x="10" y="10" width="260"
 height="210"
```
```