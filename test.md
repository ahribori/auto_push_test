# ![](https://api.ahribori.com/image/KsUWhI2entSqVSIUp4Guvvhm.png)

# SCSS 설정은 생략~

### _mixin.scss

```css
$breakpoints: (
        'small': (max-width: 767px),
        'medium': (max-width: 992px),
        'large': (max-width: 1200px),
) !default;

@mixin respond-to($breakpoint) {
    // If the key exists in the map
    @if map-has-key($breakpoints, $breakpoint) {
        // Prints a media query based on the value
        @media #{inspect(map-get($breakpoints, $breakpoint))} {
            @content;
        }
    }
    // If the key doesn't exist in the map
    @else {
        @warn "Unfortunately, no value could be retrieved from `#{$breakpoint}`. "
        + "Available breakpoints are: #{map-keys($breakpoints)}.";
    }
}
```

$breakpoints 변수에 small, medium, large 등의 도메인을 정의해 놓고, (max-width: ) 에다가 너비 몇 픽셀까지를 이 도메인으로 정의할 것인지 정의한다.

## App.scss

```css
@import './mixin';

div {
    background: white;
    @include respond-to('large') {
        background: pink;
    }
    @include respond-to('medium') {
        background: orange;
    }
    @include respond-to('small') {
        background: blue;
    }
}
```

respont-to 믹스인을 정의해놓은 _mixin.scss 파일을 import한 다음, 

div 태그에다가 테스트로 코딩을 해보자.

먼저 풀 사이즈일때는 white,

large 사이즈 영역일 때는 pink, medium 사이즈일 때는 orange, small 사이즈일 때에는 blue 색상을 배경색으로 정의한다.

여기서 주의할 점은 큰 화면에서 작은화면 순으로 위에서 아래로 코딩해야 제대로 작동한다.

개꿀!