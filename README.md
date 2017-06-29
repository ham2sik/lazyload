# image lazy load

`lazyUIT.js`를 호출하고, 상황에 따라 스크롤에 따라 이미지를 지연하는 방식(case 1)과 이미지를 한번에 다 불러오는 방식(case 2)를 사용할 수 있다.

```html
<body>

<script src="lazyUIT.min.js"></script>
<script>
  $(window).load(function() {
    // case 1 : lazyUIT.image(option);
    lazyUIT.image({
      offset: 1500,
      errorSrc: 'http://.../error_image.png',
      callback: function (element, op) {
        console.log(element, 'has been loaded')
      }
    });

    // case 2
    // lazyUIT.renderAll();
  });
</script>
</body>
```

## option

#### offset
Type: `Number`, Default: 0

값이 `0`이면 이미지요소가 뷰포트에 표시되면 이미지를 로드합니다. 특정 값(ex `1500`)을 넣으면, 뷰포트 위 또는 아래 특정 값(`1500`)부터 이미지를 로드합니다.

다음과 같이 옵션값을 변경할 수 있다.

#### errorSrc

Type: `String`, Default: `'http://.../error_image.png'`

이미지 로드에 실패하였을 경우 불러올 에러 이미지 경로

#### callback

Type: `Function`

## image case

#### case 1 : img 태그 방식

`img` 태그에 로딩할 이미지 경로를 `data-original`에, 로딩시 보일 디폴트 이미지를 `src`에 넣는다.

```html
<!-- 입력 소스 -->
<img data-original="http://.../original_image.png" src="http://.../default_image.png" alt="" />

<!-- lazy 실행 후 변환된 소스 -->
<img src="http://.../original_image.png" alt="" />
```

#### case 2 : style 태그 방식

태그에 로딩할 이미지 경로를 `data-bg-original`로 넣으면, `style='background-image: url("http://.../image.png");'`로 변환해줌

```html
<style>
  .case2 {width: 60px;height: 58px;background-size: 60px 58px;}
</style>

<!-- 입력 소스 -->
<div class="case2" data-bg-original="http://.../original_image.png"></div>

<!-- lazy 실행 후 변환된 소스 -->
<div class="case2" style='background-image: url("http://.../original_image.png");'></div>
```

#### case 3 : css 방식

`lazyBg` 클래스 사용하여 클래스가 있을 경우에는 이미지를 로드하지 않고, 클래스가 없을 경우에 이미지를 로드하도록 `css`를 작성함

```html
<style>
  .case3 {width: 60px;height: 58px;background:url("http://.../original_image.png") 0 0 no-repeat;background-size: 60px 58px;}
  .case3.lazyBg {background: none;}
</style>

<!-- 입력 소스 -->
<div class="case3 lazyBg"></div>

<!-- lazy 실행 후 변환된 소스 -->
<div class=" case3 "></div>
```

<br>
# js lazy load

`url`과 `callback`을 변수로 받아 `js`의 로딩 시점을 조절할 수 있다.

```html
<body>

<script src="lazyUIT.min.js"></script>
<script>
  $(window).load(function() {
    // lazyUIT.js(url, callback function);
    lazyUIT.js("http://.../swiper.min.js", function() {
      var swiperEvent = new Swiper('#event', {
        slidesPerView: 'auto',
        freeMode: true,
        onTouchMove: function(swiper) {
          lazyUIT.render();
        }
      });
    });
  });
</script>
</body>
```

## option

#### url

Type: `String`

#### callback

Type: `Function`

<br>
# js lazy load(Promise)

`Promise` 사용해야하는 경우

```html
<body>

<script type="text/javascript" src="lazyUIT.min.js"></script>
<script>
  $(window).load(function() {
    //lazyUIT.jsPromise(url) + Promise.all
    Promise.all([lazyUIT.jsPromise("http://.../raphael-min.js"), lazyUIT.jsPromise("http://.../recruit.js")]).then(function (values) {
      recruit.drawGenderChart();
      //console.log(values);
    });
  });
</script>
</body>
```

## option

#### url

Type: `String`

<br>
# YouTube lazy load

js url과 callback을 변수로 받아 js의 로딩 시점을 조절할 수 있다.

```html
<body>

<script type="text/javascript" src="lazyUIT.min.js"></script>
<script>
  $(window).load(function() {
    // lazyUIT.youTube(element);
    lazyUIT.youTube();
  });
</script>
</body>
```

```html
<!-- 입력 소스 -->
<div class="lazyYoutube" data-src="https://www.youtube.com/embed/gyfqeBJeWxc" data-title="I want you to die" data-options='{"width":"560", "height":"315"}'></div>

<!-- lazy 실행 후 변환된 소스 -->
<div class="lazyYoutube"><iframe width="560" height="315" title="I want you to die" src="https://www.youtube.com/embed/gyfqeBJeWxc" frameborder="0" allowfullscreen></iframe></div>
```

## option

#### js: element

Type: `String`, Default: `'.lazyYoutube'`

#### html: data-src

Type: `String`

youtube 동영상 iframe url

#### html: data-title

Type: `String`

youtube 동영상 iframe title

#### html: data-options

Type: `Object`

youtube 동영상 옵션값(`width`, `height`, `allowfullscreen` 등)






