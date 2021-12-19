---
layout: post
title: "Flutter TTRPG Blog note"
subtitle: "A flutter project for TTRPG character creation and skill/status check"
date: 2021-12-18 10:09:16 -0400
background: '/img/posts/02.jpg'
tags: [Personal Project, Flutter, Web]
---

## Project Link:

[https://glocktian.github.io/ttrpg_web_github_page/](https://glocktian.github.io/ttrpg_web_github_page/#/)

## Logical Pixel:

in the flutter documentation we have for the [size](https://api.flutter.dev/flutter/widgets/MediaQueryData/size.html) property:

Logical pixels are roughly the same visual size across devices. Physical pixels are the size of the actual hardware pixels on the device. The number of physical pixels per logical pixel is described by the [devicePixelRatio](https://api.flutter.dev/flutter/widgets/MediaQueryData/devicePixelRatio.html).

This helps us to have roughly the same size across devices.

## Elements in web and mobile

Web: top navbar, 

mobile:  drawer, bottom Navigation Bar, floating action button

can have in common: top navbar, side navbar(drawer in mobile)

## Different ways in making a grid-liked structure

Option 1: GridView

```dart
GridView.count(
  // Create a grid with 2 columns. If you change the scrollDirection to
  // horizontal, this produces 2 rows.
  crossAxisCount: 2,
  // Generate 100 widgets that display their index in the List.
  children: List.generate(100, (index) {
    return Center(
      child: Text(
        'Item $index',
        style: Theme.of(context).textTheme.headline5,
      ),
    );
  }),
);
```

Note it might be tricky to adjust the height of the item in GridView, the key is childAspectRatio, where it can be set as `childAspectRatio: (itemWidth / itemHeight),` This can be annoying when we want it to be adjusted based on the children's size.

Option2: row in listView

using ListView means we don't need to worry about the childAspectRatio when we want to set the height.

```dart
ListView.builder(
	itemCount: (items.length/2).ceil(),
	itemBuilder: (BuildContextcontext,intindex){
	      return Row(
	mainAxisSize: MainAxisSize.max,
	mainAxisAlignment: MainAxisAlignment.spaceAround,
	children: [
	          SizedBox(
	width:MediaQuery.of(context).size.width/2,
	child: EditProperty(property:items[index*2],onChanged:widget.onChanged)),
	          (index*2+1>=items.length)
	              ?SizedBox(width: MediaQuery.of(context).size.width/2,)
	              :SizedBox(
	width:MediaQuery.of(context).size.width/2,
	child: EditProperty(property:items[index*2+1],onChanged:widget.onChanged)),
	        ],
	      );
	    }
),
```

But notice it is hard to deal with index in this method, the code may get too complicated for a simple tasks.

Notice that Option 1 and 2 can both handle large number of items (or even infinite), because they build children on demand.

Option3: Wrap

Wrapping a list of widget using Wrap widget is feasible for small list. 

```dart
SingleChildScrollView(
child: Wrap(
children:
    List<Widget>.generate(widget.properties.length, (intindex) {
      double singleWidth =size.width<size.height? (size.width- 64) / 2:(size.width/2 - 64) / 2;
      return SizedBox(
width: singleWidth,
child: EditProperty(property:widget.properties[index],onChanged:widget.onChanged));
    }),
  ),
);
```

Wrap works similar to Column or Row, but it works when we run out of room at the end of Column or Row. 

The common use cases are chips or buttons, where the number of elements are relatively small, and the children items required to be displayed every thing all at once.

Option4: Third Party Library

Using package from [pub.dev](http://pub.dev) here we have an example from [https://github.com/fluttercandies/waterfall_flow](https://github.com/fluttercandies/waterfall_flow)

where we can have the waterfall grid

```dart
WaterfallFlow.builder(
	//cacheExtent: 0.0,
	padding: EdgeInsets.all(5.0),
	itemCount: data.docs.length,
	gridDelegate:
	      SliverWaterfallFlowDelegateWithFixedCrossAxisCount(
	crossAxisCount: 2,
	crossAxisSpacing: 5.0,
	mainAxisSpacing: 5.0,
	lastChildLayoutTypeBuilder: (index) =>
	index== data.docs.length
	? LastChildLayoutType.foot
	: LastChildLayoutType.none,
	  ),
	itemBuilder: (BuildContextcontext, intindex) {
	    return CharacterCard(
	character: data.docs[index].data(),
	    );
	  },
);
```

Notice that in flutter, [pub.dev](http://pub.dev) is a good place to go to, when you want to start.

## Cropping image

There are quite a number of packages from [pub.dev](http://pub.dev) that allow features for cropping images, but note that some packages may not support all devices.

There are a number of cropping 

## Deployment

```bash
flutter build web --release --base-href /ttrpg_web_github_page/ --web-renderer html
```

the base-href is not / in my case, as I didn't use the default GitHub page [which has been used for blog post]. I change it to the repo name instead of just /.