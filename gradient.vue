   <!-- Gradient -->
        <h5>Gradient</h5>
        <b-row class="mt-2">
          <b-col sm="3">
            <p>Angle</p>
          </b-col>
          <b-col sm="9">
            <b-form-input
              id="range-1"
              v-model="angleGradient"
              type="range"
              min="0"
              max="180"
              @change="changeGradient()"
            ></b-form-input>
            <div class="mt-2">
              Value: <b>{{ angleGradient }}</b>
            </div>
          </b-col>
        </b-row>
        <b-row class="mt-2">
          <b-col sm="3">
            <p>Opacity</p>
          </b-col>
          <b-col sm="9">
            <b-form-input
              id="range-1"
              v-model="opacityGradient"
              type="range"
              min="0"
              max="100"
              @change="changeGradient()"
            ></b-form-input>
            <div class="mt-2">
              Value: <b>{{ opacityGradient }}</b>
            </div>
          </b-col>
        </b-row>
        <!-- /Gradient -->


         angleGradient: number = 120;
  opacityGradient: number = 100;

handleGradientChange(){
    const anglePI = (180 - this.angleGradient) * (Math.PI / 180);
    const angleCoords = {
      x1: Math.round(50 + Math.sin(anglePI) * 50) / 100,
      y1: Math.round(50 + Math.cos(anglePI) * 50) / 100,
      x2: Math.round(50 + Math.sin(anglePI + Math.PI) * 50) / 100,
      y2: Math.round(50 + Math.cos(anglePI + Math.PI) * 50) / 100,
    };

    const gradient = {
      type: 'linear',
      gradientUnits: 'percentage',
      coords: {
        x1: angleCoords.x1 || 0,
        y1: angleCoords.y1 || 0,
        x2: angleCoords.x2 || 0,
        y2: angleCoords.y2 || 0,
      },
      colorStops: <any>[
        { offset: 0, color: 'black', opacity: this.opacityGradient / 100 },
        { offset: 1, color: 'yellow', opacity: this.opacityGradient / 100 },
      ],
    };
    console.log(gradient);
    return gradient;
  };

  changeGradient(){
    // console.log('this.activeObject', this.activeObject);
    this.activeObject.set(
      'fill', 
      new fabric.Gradient(this.handleGradientChange())
      );
    
    // this.activeObject.fill = new fabric.Gradient(this.handleGradientChange());
    
    this.requestRenderAll();
  }