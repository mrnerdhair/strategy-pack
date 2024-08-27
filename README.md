# Strategy Pack

[![Open in HACS at your Home Assistant instance.][hacsBadge]][strategyPackHacs]

This is a collection of [Home Assistant Strategies](https://developers.home-assistant.io/docs/frontend/custom-ui/custom-strategy/).

A strategy is Javascript code that gets executed to create Dashboards and Views automatically. They make it easy to have auto-populated Dashboards with next to no configuration!

The strategies can be at the dashboard level, generating whole dashboards with multiple views:

```yaml
strategy:
  type: custom:example-dashboard-strategy
  #The Config for this dashboard dependant on the view; nothing to do with HA Config
  config: config for this dashboard
#The Home Assistant View Options like:
##Currently i think there are none for dashboards
```

or at the view level, generating a single view in an already existing dashboard.

```yaml
views:
  - strategy: 
      type: custom:example-view-strategy
      #The Config for this view dependant on the view; nothing to do with HA Config
      config: config for this view
    #The Home Assistant View Options like:
    ##icon: mdi-example
    ##path: example
    ##title: Example
    ##visible:
    ##  - user_you_want
  - other views you want...
```

The collection currently consists of 3 Strategies (with Area Dashboard Strategy being the main one), but I just started and am looking forward to adding more if there's demand.

>[!NOTE]
>If you want to sort anything in the strategies, you can use "Label Sort".<br>
>It works currently on areas (=sort of navigation areas and views overall) and entities (=sort in the grid).<br>
>Just create Labels with the exact name as below (Sort:1, Sort:2, ... as many as you want) and assign them.<br>
>![Label Sort](/documentation/assets/area/area-strategy-label-sort.png "Label Sort")

## Installation

[Installation Instructions here](./documentation/markdown/INSTALLATION.md)

## 1. Area Dashboard Strategy

Fully configurabe Dashboard with View per Area and auto-populating entities ordered in Grids.

 ![Area Strategy](/documentation/assets/area/area-strategy.gif "Area Strategy")
 
 The dashboard was designed to be fully responsive! You can absolutely use this also on tablets or phones!

 ![Area Strategy Responsive](/documentation/assets/area/area-strategy-responsive-new.gif "Area Strategy Responsive")

The Dashboard contains all entities assigned to that Area (either via device or entity itself).

 You may not be able to tell it generates multiple Views because all but one are made invisible in the top menu.

 ![Top Menu](/documentation/assets/area/area-strategy-top-menu.png "Top Menu")

This is because the navigation is meant to be made with the left-sided navigation menu.

[More on the Design: UI explained](./documentation/markdown/area/UI.md)

### Usage

You need to create a new empty Dashboard for this Strategy Dashboard.

Dashboard -> Edit Dashboard -> Raw Configuration Editor (kebap menu) -> Paste the following

```yaml
strategy:
  type: custom:area-dashboard-strategy
```

This will create a Dashboard with multiple Views for your specific Areas.

### Configuration

This Strategy is completely configurable.
Modifications are possible to:

- the left-sided navigation menu (modifications to the area-card)
- the tabs in the main area (number of tabs, their names, icons, etc.)
- the content of the tabs (number of grids, header, cards in the grids, etc.)

Configuration works like this:

```yaml
strategy:
  type: custom:area-dashboard-strategy
  config:
    #Your Config here like:
    tabs: ...
```

[All Configration Options here](./documentation/markdown/area/CONFIGURATION.md#configuration)

There is a sensible default configuration, which is the one i myself use.
So you can start out without configuring anything and have a nice dashboard.
And if you find something you don’t like, just start configuring!

[Default Configuration explained](./documentation/markdown/area/CONFIGURATION.md#default-config-explained)

## 2. Grid View Strategy

Strategy fully customizable with custom rows. You can create auto-populating Dashboards where you can display anything you like with little configuration! Could be used to implement Battery/Update Strategy or something like that.

 ![Grid View Strategy](/documentation/assets/grid/grid-view-strategy.png "Grid View Strategy")

### Usage

You add this to already existing dashboards as an extra view.

Dashboard -> Edit Dashboard -> Raw Configuration Editor (kebap menu) -> Add the following

```yaml
... (existing dashboard)
views:
  - strategy:
      type: custom:grid-view-strategy
      config:
        rows:
          - this one needs configuration!
    title: YourTitle
    icon: mdi:youricon
    path: yourpath
```

This Strategy is completely configurable.
Modifications are possible to:

- the rows/grids in the view (number of grids, header, etc.)

Configuration works like this:

```yaml
  - strategy:
      type: custom:update-view-strategy
      config:
        #Your Config here like:
        rows:
          - row 1 config
          - row 2 config
    title: YourTitle
    icon: mdi:youricon
    path: yourpath
```

[All Configration Options here](./documentation/markdown/grid/CONFIGURATION.md#configuration)

## 3. Battery View Strategy

View Strategy with one page for all battery entities.

 ![Battery View Strategy](/documentation/assets/battery/battery-view-strategy.png "Battery View Strategy")

### Usage

You add this to already existing dashboards as an extra view.

Dashboard -> Edit Dashboard -> Raw Configuration Editor (kebap menu) -> Add the following

```yaml
... (existing dashboard)
views:
  - strategy:
      type: custom:battery-view-strategy
    title: YourTitle
    icon: mdi:youricon
    path: yourpath
```

This Strategy is completely configurable.
Modifications are possible to:

- the rows/grids in the view (number of grids, header, etc.)

Configuration works like this:

```yaml
  - strategy:
      type: custom:battery-view-strategy
      config:
        #Your Config here like:
        platforms: ...
    title: YourTitle
    icon: mdi:youricon
    path: yourpath
```

[All Configration Options here](./documentation/markdown/battery/CONFIGURATION.md#configuration)

## 4. Update View Strategy

View Strategy with one page for all update entities.

 ![Update View Strategy](/documentation/assets/update/update-view-strategy.png "Update View Strategy")

### Usage

You add this to already existing dashboards as an extra view.

Dashboard -> Edit Dashboard -> Raw Configuration Editor (kebap menu) -> Add the following

```yaml
... (existing dashboard)
views:
  - strategy:
      type: custom:update-view-strategy
    title: YourTitle
    icon: mdi:youricon
    path: yourpath
```

This Strategy is completely configurable.
Modifications are possible to:

- the rows/grids in the view (number of grids, header, etc.)

Configuration works like this:

```yaml
  - strategy:
      type: custom:update-view-strategy
      config:
        #Your Config here like:
        platforms: ...
    title: YourTitle
    icon: mdi:youricon
    path: yourpath
```

[All Configration Options here](./documentation/markdown/update/CONFIGURATION.md#configuration)

## Credits

Thanks to everyone working on Home Assistant and the everyone in the community. Without your documentation, code, and forum posts, I wouldn't have even thought about this.

The design is heavily inspired by [Dwains Dashboard][dwainsDashboard], as that the first more advanced dashboard i used because the design and auto-population really hit a nerve with me. I wanna thank Dwain for his great work. His Dashboard is more User-friendly and works without any yaml-Knowledge so it is absolutely a better fit for many Users. Give it a try!

Also have a look at [Mushroom Strategy][mushroomStrategy], which has a very similar concept to the Area Strategy. I must admit i also shamelessly copied their installation instructions.

<!-- Badge References -->
[hacsBadge]: https://my.home-assistant.io/badges/hacs_repository.svg
<!-- URL References -->
[strategyPackHacs]: https://my.home-assistant.io/redirect/hacs_repository/?owner=itsteddyyo&repository=strategy-pack&category=lovelace
<!-- Credit References -->
[dwainsDashboard]: https://github.com/dwainscheeren/dwains-lovelace-dashboard
[mushRoomStrategy]: https://github.com/AalianKhan/mushroom-strategy
