---
title: Show directions with Azure Maps | Microsoft Docs
description: How to display directions between two locations on a Javascript map
author: jingjing-z
ms.author: jinzh
ms.date: 11/15/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: timlt
ms.custom: codepen
---

# Show directions from A to B

This article shows you how to make a route request and show the route on the map.

There are two ways to do so. The first way is to query the [Azure Maps Route API](https://docs.microsoft.com/rest/api/maps/route/getroutedirections) through a service module. The second way is to make a [XMLHttpRequest](https://xhr.spec.whatwg.org/) to the API. Both ways are discussed below.

## Query the route via service module

<iframe height='500' scrolling='no' title='Show directions from A to B on a map (Service Module)' src='//codepen.io/azuremaps/embed/RBZbep/?height=265&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/RBZbep/'>Show directions from A to B on a map (Service Module)</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

In the code above, the first block of code constructs a Map object. You can see [create a map](./map-create.md) for instructions.

The line in the second block of code instantiates a client service.

The third creates and adds a [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) object to the map.

 A line is a [Feature](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.feature?view=azure-iot-typescript-latest) of LineString. A [LineLayer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.layer.linelayer?view=azure-iot-typescript-latest) renders line objects wrapped in the  [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) as lines on the map. The fourth block of code creates and add a line layer to the map. See properties of a line layer at [LinestringLayerOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.linelayeroptions?view=azure-iot-typescript-latest).

A [symbol layer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.layer.symbollayer?view=azure-iot-typescript-latest) uses text or icons to render point-based data wrapped in the [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) as symbols on the map. The fifth block of code creates and add a symbol layer to the map.

The sixth block of code creates start and end [points](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.data.point?view=azure-iot-typescript-latest) object and adds them to the dataSource object.

The seventh block of code sets the bounds of the map using the Map's [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera-cameraoptions---cameraboundsoptions---animationoptions-) property.

The last block of code queries the Azure Maps routing service, which is part of the [service module](https://atlas.microsoft.com/sdk/js/atlas-service.js?api-version=1). The [getRouteDirections](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.models.routedirectionsrequestbody?view=azure-iot-typescript-latest) method is used to get a route between the start and end points. The response is then parsed into GeoJSON format using the [getGeoJsonRouteDirectionsResponse](https://docs.microsoft.com/javascript/api/azure-maps-rest/atlas.service.routegeojson?view=azure-iot-typescript-latest) method. It then renders the response as a route on the map. For more information about adding a line to the map, see [add a line on the map](./map-add-shape.md#addALine).

The route query, data source, symbol, and line layers and the camera bounds are created and set within the map's [event listener](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#events) to ensure that the results are displayed after the map loads fully.

## Query the route via XMLHttpRequest

<iframe height='500' scrolling='no' title='Show directions from A to B on a map' src='//codepen.io/azuremaps/embed/zRyNmP/?height=469&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/azuremaps/pen/zRyNmP/'>Show directions from A to B on a map</a> by Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

The first block of code constructs a Map object. You can see [create a map](./map-create.md) for instructions.

The second block of code creates and adds a [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) object to the map.

The third code block creates the start and destination points for the route and adds them to the data source. You can see [add a pin on the map](map-add-pin.md) for instructions about using [addPins](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest).

 A [LineLayer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.layer.linelayer?view=azure-iot-typescript-latest) renders line objects wrapped in the  [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) as lines on the map. The fourth block of code creates and adds a line layer to the map. See properties of a line layer at [LineLayerOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.linelayeroptions?view=azure-iot-typescript-latest).

A [symbol layer](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.layer.symbollayer?view=azure-iot-typescript-latest) uses text or icons to render point-based data wrapped in the [DataSource](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.source.datasource?view=azure-iot-typescript-latest) as symbols on the map. The fifth block of code creates and add a symbol layer to the map. See properties of a symbol layer at [SymbolLayerOptions](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.symbollayeroptions?view=azure-iot-typescript-latest).

The next code block creates `SouthWest` and `NorthEast` points from the start and destination points and sets the bounds of the map using the Map's [setCamera](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#setcamera-cameraoptions---cameraboundsoptions---animationoptions-) property.

The last block of code sends an [XMLHttpRequest](https://xhr.spec.whatwg.org/) to [Azure Maps Route API](https://docs.microsoft.com/rest/api/maps/route/getroutedirections). It then parses the incoming response. And for a successful response, it collects the latitude and longitude information for each route point and  creates an array of lines by connecting those points. It then adds all those lines onto the dataSource to render the route on the map. You can see [add a line on the map](./map-add-shape.md#addALine) for instructions.

The route query, data source, symbol, and line layers and the camera bounds are created and set within the map's [event listener](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest#events) to ensure that the results are displayed after the map loads fully.

## Next steps

Learn more about the classes and methods used in this article:

> [!div class="nextstepaction"]
> [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)

See the following articles for full code examples:

> [!div class="nextstepaction"]
> [Show traffic on the map](./map-show-traffic.md)

> [!div class="nextstepaction"]
> [Interacting with the map - mouse events](./map-events.md)
