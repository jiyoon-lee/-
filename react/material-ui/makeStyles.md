# makeStyles
```javascript
import { makeStyles } from '@material-ui/core/styles'
```
makeStyles는 @material-ui/core/styles에서 import 해 사용한다.<br>
그럼 @material-ui/core/styles는 무엇일까.<br>
@material-ui/core/styels는 Material-UI의 스타일 솔루션이다.<br>
이전에 Material-UI는 component 스타일 작성을 위해 사용자 정의 inline style solution인 LESS를 사용했지만, 이러한 접근 방식은 제한적이라는 것을 입증했습니다.<br>
CSS-in_JS solution은 이 한계를 극복하고 이 밖에(theme nesting, dynamic styles, self-support 등)의 기능을 지원합니다.<br>

예시를 통해 @material-ui/core/styles를 사용해보자.<br>
아래의 3가지 예시는 모두 동일한 기본 논리를 공유한다.<br>
1. Hook API
```javascript
import React from 'react'
import { makeStyles } from '@/material-ui/core/styles'
import Button from '@/material-ui/core/Button'

const useStyles = makeStyles({
  root: {
      background: 'linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)'
  }
export default function Hook () {
  const classes = useStyles()
  return <Button className={classes.root}Hook</Button>
}
```

2. Styled components API
이것은 오직 호출 구문에만 적용된다. 스타일 정의는 여전히 JSS객체를 사용한다. 일부 제한과 함께 이 동작을 변경할 수도 있다.
```javascript
import { styled } from '@/material-ui/core/styles'
import Button from '@material-ui/core/Button'

const MyButton = styled(Button) ({
  background: 'linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%'),
 })
 
export default function StyledComponents() {
  return <MyButton>Styled Components</MyButton>
}
```

3. Higher-order component API
```javascript
import PropTypes from 'prop-types'
import { withStyles } from '@material-ui/core/styles'
import Button from '@material-ui/core/Button'
const styles = {
  root: {
    background: 'linear-gradient(45deg, #FE6B8B 30%, #FF8E53 90%)'
  }
}
function HigherOrderComponent(props) {
  const { classes } = props
  return <Button className={classes.root}>Higher-order component</Button>
}
HigherOrderComponent.propTypes = {
  classes: PropTypes.object.isRequired,
)
export default withStyles(styles) (HigherPrderComponent)
```

Nesting selectors<br>
선택자를 현재 클래스 또는 컴포넌트 내부의 대상요소에 중첩시킬 수 있다. <br>
다음 예제에서는 Hook API를 사용하지만 다른 APU에서도 동일한 방식으로 작동한다.<br>
```js
const useStyles = makeStyles({
  root: {
    color: 'red',
    '& p': {
      color: 'green',
        '& span;: {
          color: 'blue'
       }
     }
   }
})
```

Adaptin based on props<br>
컴포넌트의 특성에 따라 생성된 값을 조정하기 위해 스타일(보간)을 만드는 함수를 전달할 수 있다.<br>
이 함수는 스타일 규칙 수준 또는 CSS특성 수준에서 제공될 수 있다.
```javascript
const useStyles = makeStyles({
  foo: props => ({
    backgroundColor: props.backgroundColor,
  }),
  bar: {
    color: props => props.color,
  })
})
function MyComponent () {
  const props = { backgroundColor: 'black', color: 'white' }
  const classes = useStyles(props)
  return <div className={`${classes.foo} ${classes.bar}`} />
```
