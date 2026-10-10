```
<mx:GridItem>
<mx:GridItem width="100%" height="100%">
<mx:Text width="130" id="hireTxt"
text="{emp.getItemAt(0).HIREDATE}"
fontFamily="Verdana" color="#060EAF"/>
</mx:GridItem>
</mx:GridRow>
<mx:GridRow width="100%" height="100%">
<mx:GridItem width="100%" height="100%">
<mx:Label text="Department" color="#2553BB"
fontWeight="bold" fontSize="13"
fontStyle="normal" textAlign="right"/>
</mx:GridItem>
<mx:GridItem width="100%" height="100%"
color="#060EAF">
<mx:Text text="{emp.getItemAt(0).DEPT}" id="text2"
fontFamily="Verdana"/>
</mx:GridItem>
</mx:GridRow>
<mx:GridRow width="100%" height="100%">
<mx:GridItem width="100%" height="100%">
<mx:Label text="Job" color="#2553BB" fontSize="13"
fontWeight="bold" textAlign="right" width="33"/>
</mx:GridItem>
<mx:GridItem width="100%" height="100%"
fontFamily="Verdana">
<mx:Text text="{emp.getItemAt(0).JOB}"
color="#060EAF"/>
</mx:GridItem>
</mx:GridRow>
<mx:GridRow width="100%" height="100%">
<mx:GridItem width="100%" height="100%">
<mx:Label text="Salary" color="#2553BB"
fontSize="13" fontWeight="bold"
textAlign="right"/>
</mx:GridItem>
<mx:GridItem width="100%" height="100%">
<mx:Text text="{emp.getItemAt(0).SALARY}"
fontFamily="Verdana" color="#060EAF"/>
</mx:GridItem>
</mx:GridRow>
<mx:GridRow width="100%" height="100%">
<mx:GridItem width="100%" height="100%">
<mx:Label text="Phone No" color="#2553BB"
```