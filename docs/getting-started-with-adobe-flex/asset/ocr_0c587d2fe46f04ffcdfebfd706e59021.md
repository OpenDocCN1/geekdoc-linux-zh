```
private function init() {
ProfitChart.addEventListener(ChartItemEvent.ITEM_CLICK, onItemClick);
}
```

Listing 8.19 – Click event listener

11. In the above code snipet, the onItemClick method is the event handler function and has to be defined. Say you have an XML file for each month for the distribution of profit across business sectors. For example, Oct.xml has the data for the month of October and likewise for the other months. An example of the data in these files is shown in *Listing 8.20* below.

```
<?xml version="1.0" encoding="utf-8"?>
<items>
<item industry="Textiles" value="30" />
<item industry="Agriculture" value="50" />
<item industry="Manufacturing" value="20" />
</items>
```

Listing 8.20 – Detail data for a specific month

12. In the itemClick handler, you will send an HTTP request to get the data from these XML files depending on which month's data you require. You can use the HitData object to obtain what data was underneath the mouse when the event was triggered as shown in *Listing 8.21* below.

```
private function onItemClick(event:ChartItemEvent):void{
var month:String= event.hitData.item.month;
var request:HTTPService = new HTTPService();
request.url = "data/"+month+".xml";
request.addEventListener(FaultEvent.FAULT,onFaultEvent);
request.addEventListener(ResultEvent.RESULT,onResultEvent);
request.send();
}
```

Listing 8.21 – click event handler function

13. The result event handler for the HTTP request made above should redefine the data provider for the chart and set up the axes according to the data to be displayed as shown in *Listing 8.22* below.

```
private function onResultEvent (event:ResultEvent) {
stats = event.result.items.item;
ProfitChart.dataProvider=stats;
series.xField="industry";
series.yField="value";
axis.categoryField="industry";
}
```

Listing 8.22 – Function to redefine values