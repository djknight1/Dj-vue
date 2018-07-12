# Dj-vue
my vue repository of components
#It can be installed by npm `npm: npm install dj_slider`
# It has only two components now
1:Slider:  
`import {Slider} from 'dj_slider'`

`  components: {
    Slider
  }`
  
  ```
    <section class="section">
      <div class="slider">
        <slider :images="images"></slider>
      </div>
  ```
  
  
  It can recieves 4 props now.Including images,loop,speed and autoplay.
  !()
   ```
   images: {  
                type: Array,
                default: () => []
            },  
            loop: {
                type: Boolean,         
                default: true
            },  
            
            speed: {
                type: Number,
                default: 2000
            },  
            
            autoplay: {
                type: Boolean,
                default: true
            },
     ```
     
2: Thumbnail:
    Its so easy.... It only need a 1 prop which is thumbnails(I know its a bad name...)
