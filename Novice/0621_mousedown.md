# mousedown과 click의 event 시점

[A**** B***]

```pug
.sender-input-wrapper
            input.sender-input(placeholder="이름으로 검색" @keyup.enter="searchUserByName" v-model="searchUserInput"
            @focus="isOpenInput=true" @blur="onBlur")
            .list-wrapper(v-show="isOpenInput")
              .list-line(v-for="searcUser in serachUserList" @click="e => selectShareUser(e,searcUser)")
                .list-name-text {{searcUser.name}}
                .list-info-text {{searcUser.deptname}}
```

input의 입력 내용으로 input 하단에 검색 결과 리스트가 나오는 component를 만들고 있었다.

## 문제상황

input에 blur/focus event를 통해서 리스트 open을 컨트롤 했다. 그리고 하단 리스트에서 결과물 선택을 click event로 잡았다.

하지만 결과물 선택시에 blur가 click보다 먼저 잡혀서 click event가 발생을 못 했다.

## 실수/착각

click은 마우스를 out하는 순간 발생한다. 즉, 손을 뗄 때 발생한다.

## 해결방안

**click**이 아니라 **mousedown**으로 event를 잡았어야한다. **mousedown**은 마우스를 누르는 순간에 잡힌다.
