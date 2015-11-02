## at-core-resize-sensor

at-core-resize-sensor is a component that tracks its parent's width and triggers
`resize-sensed` event when parent's width changes.

#### How to use:
```
<dom-module id="demo-component">
  <style>
    .wrapper {
      position: relative;
    }

    .clear-float {
      clear: both;
    }
  </style>
  <template>
    <div class="wrapper">
      <at-core-resize-sensor id="resizeSensor"></at-core-resize-sensor>
      <div class="clear-float"></div>
      <div>
        ... your content goes here
      </div>
    </div>
  </template>
  <script>
    Polymer({
      is: 'demo-component',
      attached: function () {
        var resizeSensor = this.$.resizeSensor;
        var initialWidth = resizeSensor.queryWidth();
        resizeSensor.addEventListener('resize-sensed', function (event) {
          var updatedWidth = event.detail.value.width;

          ... use updatedWidth value here
        });
      }
    });
  </script>
</dom-module>
```

#### 1. Put at-core-resize-sensor inside a relatively positioned wrapper
This is needed because at-core-resize-sensor uses a absolutely positioned and floated element to fill its parent's width, so width can be measured
#### 2. Put a div with style="clear: both" after at-core-resize-sensor
This tells the browser to correctly layouts the elements so that they have correct widths
#### 3. Listen on `resize-sensed` event of at-core-resize-sensor
Attach to `resize-sensed` event to be notified when width of the parent changes.
#### 4. Initial width of the parent
Inside `attached` callback call at-core-resize-sensor.queryWidth function to get the initial width of the parent.
#### 5. Enjoy life
